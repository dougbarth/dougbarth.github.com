---
layout: post
title: Rabbit on a Leash — Rate Limited AMQP subscriptions
---

[RabbitMQ](http://www.rabbitmq.com) is fast: [really fast](http://www.rabbitmq.com/faq.html#performance). Consuming messages from a queue is extremely efficient. Consumers declare the queues they are subscribing to and the broker pushes messages to the consumer for processing as soon as they are ready. The [AMQP protocol](http://www.amqp.org), which RabbitMQ implements, supports the concept of limiting how many outstanding messages a consumer can be tasked with processing via the `prefetch_count` and `no_ack` headers, but it does not have a way to control the rate of delivery of messages to consumers.

At [Signal](http://www.signalhq.com), we use RabbitMQ for all our queueing infrastructure needs. Outgoing SMS messages (MTs) are queued for a pool of workers to send to our aggregator. Our connection to our SMS aggregator requires us to limit the rate that we send messages to their system. It would seem that RabbitMQ is a poor fit for that use case, but we've been able to fulfill it using a bit of client side code and the existing AMQP protocol.

Using AMQP's `prefetch_count`, client acks and a blocking token bucket, it's possible to implement rate controlled processing of queued messages.

## Token Buckets

A token bucket is an algorithm that is used to control the rate of data that flows through a system[1]. Token buckets can be configured to allow traffic to burst to full speed, but they ensure that the average traffic processed is held at a configurable rate.

The concept of a token bucket is rather simple. Imagine the bucket in your freezer's ice maker. Cubes of ice are added to the bucket at a certain rate (say 1 a second). The size of the bucket controls how many ice cubes (tokens) we can have waiting in the bucket before we will stop making more.

In order for traffic to be processed, we need to take a token (or more) from that bucket. If the bucket is empty, that work cannot be processed. The rate that tokens are added to the bucket controls the average speed that work is processed. If we started with an empty bucket we could process work at a rate equal to the rate that we added cubes of ice. The size of the bucket controls how much work we can burst. If the bucket held 10 tokens, we could process 10 units of work at full speed before we would be rate limited.

## Putting it all together

With a correctly working token bucket, implementing fixed rate processing is fairly straightforward. First, when subscribing to a queue, we set an explicit `prefetch_count` on the channel and we set `no_ack` to false when subscribing. The `prefetch_count` limits how many unacked messages RabbitMQ will deliver and @no_ack@ allows us to acknowledge the message once we've finished processing it. In our application, we size the `prefetch_count` so there are a few seconds worth of messages waiting in the worker's memory to be sent.

We use the token bucket to control our rate of processing these messages from RabbitMQ. We need to take a token from the bucket before processing a message. If the bucket is empty, we block until a new token is added.

```ruby
EM.run do
  channel = AQMP::Channel.new

  # Allow 10 unacked messages to be delivered to this worker.
  channel.prefetch(10)

  # Configure this worker to send at 1 msg/s on average with occassional bursts
  # up to 5 messages.
  token_bucket = TokenBucket.new(1, 5)

  # Refresh the token bucket every second. The bucket is also refreshed
  # when the take method is called.
  EM.add_periodic_timer(1) { token_bucket.refresh }

  # We subscribe with explicit acknowledgments so we can signal to RabbitMQ
  # that more work should be delivered. Without this setting, RabbitMQ would
  # send work over to us as fast as possible.
  channel.queue('send_mt').subscribe(:ack => true) do |header, message|
    # Defer the processing to a background thread since taking a token from
    # the bucket could potentially be a blocking operation and we don't want to
    # block the reactor.
    EM.defer(
      lambda {
        # Takes 1 token from the bucket. If the bucket is empty, this
        # method will block.
        token_bucket.take(1)

        process_message(message)

        # Acknowledge this message, allowing RabbitMQ to send more work.
        header.ack
      }
    )
  end
end
```

fn1. "Token Buckets (Wikipedia)":http://en.wikipedia.org/wiki/Token_bucket
