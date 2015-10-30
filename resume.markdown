---
layout: resume
---

Doug Barth
============

A passionate full-stack coder. I love learning and I love producing results in the fewest lines of code.

* Github: <https://github.com/dougbarth>
* Blog: <http://dougbarth.github.com/>
* Twitter: <https://twitter.com/dougbarth>
* Email: <dougbarth@gmail.com>

Jobs
------------

### [PagerDuty] - San Franciso, CA

October 2012 - Present

Incident management software trusted by companies big and small

Titles held: Senior Operations Enginner, Senior Software Engineer

* Built a development style workflow for operations engineers working on Chef configuration changes, which allowed PagerDuty to grow the ops team and productivity with it
* Replaced PagerDuty's DRBD based MySQL tier with Percona's XtraDB Cluster, which enabled us to perform database maintenance and scaling without incurring downtime. I gave a talk at Percona Live 2015 about this setup.
* Built a host to host IPsec based mesh network, encrypting every packet that traverses the network both with the datacenter and across the WAN. I gave a talk at Velocity Santa Clara 2015 about this project.
* Rebuilt PagerDuty's disaster recovery site, adding monitoring for parity with production and funneling a portion of production traffic through the DR site to validate its correctness. I gave a talk at SRECon 2015 about this project.
* Interviewed many of PagerDuty's critical engineering hires
* Responsbile for running PagerDuty's Failure Friday program, which injects failure into the production system. I gave a talk about this process numerous times: DevOpsDays London 2013, DOD Toronto 2014, DOD Austin 2015
* Spoke at several conferences and meetups

Tech used: Chef, Ruby, Percona XtraDB Cluster (MySQL), Rails, DRBD, Linux, IPsec, memcache, nginx, HAProxy

[PagerDuty]:http://www.pagerduty.com/

### Signal Engage - Chicago, IL

May 2008 - October 2012

Easy to use Text, Social & Email marketing tools. The business was bought and the product is now retired.

Titles held: Lead Architect

* 2nd full time engineer, 4th employee
* Responsible for designing, developing and maintaining the full system
* Built a system that powered SMS text to win contest for on air radio stations
* Sent monthly SMS messages for Redbox to 3 million consumers with unique coupon codes at a rate of 320 messages/s
* Built a system for sending partially customizable emails from predefined templates for use by non-technical users. This was deployed by Culver's and Kum and Go across their franchises.
* Convinced our team to move to git from Subversion
* Replaced ap4r with RabbitMQ as our main queuing system
* Got us started using Puppet to manage our production boxes replacing a manual setup process
* Upgraded the application to the latest Rails version multiple times
* Wrote the entire first version of the Apartments.com iPhone App,
  helped develop the [Newser](http://itunes.apple.com/us/app/newser/id334678577?mt=8) and
  Homefinder iPhone apps
* Delivered countless projects, often under accelerated timelines
* Directly supported customers
* Mentored new engineers, getting them up to speed and providing design guidance

Tech used: Ruby, Rails, MySQL, RabbitMQ, memcached, Redis, MongoDB, CouchDB, jQuery, HTML, CSS, EventMachine, Linux, Puppet

[Signal]:http://www.signalhq.com/

### [Orbitz] - Chicago, IL

Dec 2003 - May 2008

An online travel search & booking site.

Titles held: Intern, Software engineer, Senior Software Engineer, Tech Lead

* During my 5 years there, I moved from an entry level position to a technical lead of the development tools team
* Advanced to a Senior Engineer on the Hotels team developing projects and mentoring other developers
* Worked on a side team that built a new monitoring solution for Orbitz. [ERMA] and [Graphite] are two projects that were open sourced from that system.
* Joined the Development Tools team as a tech lead
* As tech lead, I was responsible for Orbitz' Accurev (SCM), Jira, Confluence & various other development tools
* I consulted with teams on the best ways to use the tools within their teams

Tech used: Java, Spring, Spring WebFlow, EJBs, JINI, Oracle DBs, Linux

[Orbitz]:http://www.orbitz.com/

Open Source
------------

### Projects I have started
* [whazzup] --- Health check daemon that decouples service checks from client health checks
* [lita-enhance] --- ChatOps tool for replacing opaque machine identifying information with human readable info
* [jsonlint] --- Checks JSON documents for common errors
* [amqp-utils] --- Command line utils for interacting with an AMQP based queue
* [ERMA] --- Monitoring API I developed while at Orbitz (no longer involved)

### Projects I have contributed to
* [foodcritic] --- Performance enchancements
* [chefspec] --- Bug fixes
* [chef-denyhosts] --- Cookbook enhancements
* [backup] --- Added PagerDuty notifier
* [capistrano] --- Added Accurev support
* [rails] --- Fixed MySQL transaction management; Fixed ActiveSupport::Cache semantics for memcached
* [amqp] --- Some quick fixes
* [query_trace] --- Easy toggle of tracing on/off
* [Scout] plugins --- Created and contributed RabbitMQ plugins
* [parallel_tests] --- Added a way to control the number of workers from an environment variable
* [mongoid_optimistic_locking] --- Bug fixes
* [automongobackup] --- Proper exit code

Education
------------

### [Illinois Institute of Technology]

2000 - 2003: B.S. in Computer Science and B.S. in Computer Engineering (dual degree)

[Illinois Institute of Technology]:http://www.iit.edu

Interests
------------

Awesome craft beer, Foosball (practiced with a former Pro), Movies (built our own theater room), vim

[whazzup]:https://github.com/PagerDuty/whazzup
[lita-enhance]:https://github.com/PagerDuty/lita-enhance
[jsonlint]:https://github.com/dougbarth/jsonlint
[amqp-utils]:https://github.com/dougbarth/amqp-utils
[ERMA]:https://github.com/erma/erma

[foodcritic]:https://github.com/acrmp/foodcritic/commits/master?author=dougbarth
[chefspec]:https://github.com/sethvargo/chefspec/commits/master?author=dougbarth
[chef-denyhosts]:https://github.com/phlipper/chef-denyhosts/commits/master?author=dougbarth
[backup]:https://github.com/backup/backup/commits/master?author=dougbarth
[capistrano]:https://github.com/capistrano/capistrano/commit/03522bf7c1d69a4819c63a722fad4c2d309d2884
[rails]:https://github.com/rails/rails/commits/master?author=dougbarth
[amqp]:https://github.com/ruby-amqp/amqp/commits/master?author=dougbarth
[query_trace]:https://github.com/ffmike/query_trace/commits/master?author=dougbarth
[parallel_tests]:https://github.com/grosser/parallel_tests/commits/master?author=dougbarth
[automongobackup]:https://github.com/micahwedemeyer/automongobackup/commits/master?author=dougbarth
[mongoid_optimistic_locking]:https://github.com/burgalon/mongoid_optimistic_locking/commits/master?author=dougbarth

[Scout]:http://scoutapp.com/
[Graphite]:http://graphite.wikidot.com/

