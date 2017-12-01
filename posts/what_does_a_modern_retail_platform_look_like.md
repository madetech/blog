# What Does a Modern Retail Technology Platform Look Like?

Far from technology star gazing, we explore what a modern retail technology platform could look like. Established retailers are typically encumbered by a number of legacy technology choices that are deeply embedded in their business - from a creaking SAP rollout, to proprietary Warehouse Management Systems that are resistant to integration.

Starting with the customer, and with the goal of delivering a highly cohesive brand experience through multiple touchpoints, more recent competitors have been able to quickly compete with more established players, not in small part due to their ability to make modern technology choices from the outset.


## A Collection of Best of Breed Systems

Rather than trying to find an all-in-one solution to run their retailing operation, modern retailers look to combine a number of best of breed services, opting for discrete Data Warehousing, E-commerce, and Product Management packages, for example.

Key to adopting and integrating disparate systems is choosing systems that have both open and high quality APIs that expose that systems capabilites to other applications. Beware of any software vendor that sells "connectors" to integrate with other third party systems. Open APIs allow the retailer to choose how to best integrate their systems.

Amazon.com is famed for its adopting of a service oriented approach. It's reported that rendering the Amazon.com homepage involves in the region of 120 services, from recommendations, to stock availability.


## A Common Messaging System

To avoid tightly coupling software services, a common messaging system can be used to enable each service to publish new events, and to subscribe to receive particular types of events emitted by other services.

This avoids the services communicating directly, which is a pattern that often leads to tight coupling, which in turn can easily result in services becoming overly dependent on one another.

There are examples of Zalando, Etsy, and Shopify [using messaging systems](https://kafka.apache.org/powered-by) to provide a means of communication between their services.


## Clear Boundaries Between Systems

An important architectural mandate for modern retail platforms is to provide clearly defined boundaries between the various services. The responsibility of each service needs to be clearly defined, as well as how the service will interoperate with the other services in the retailer's landscape.

The boundary of each service should provide a contract that specifies the format of the events that it will emit, as well as the type of events it will respond to from other services.

Returning to the example of Amazon, one of the pivotal moments in the company's history was [Bezos' 2002 mandate](https://gigaom.com/2011/10/12/419-the-biggest-thing-amazon-got-right-the-platform/) that every business unit must expose their data and functionality via API. As well as giving rise to Amazon Web Services (currently a $16 billion revenue stream), it allows business units autonomy in solving their business problems with technology, while mandating common standards.


## A Continuously Evolving Technology Landscape

Many legacy retailers treat technology evolution as a decades apart expensive big bang upgrades and replatforms. Painful enough to avoid for as long as possible, and perhaps a little beyond.

More modern retailers shift their mindset to think of technology investment as an ongoing operational expense over a one-off capital expense, investing to improve and evolve the technology landscape as an ongoing effort.

As a modern retail platform will be comprised of a number of smaller systems, replacing individual components as they reach end of life becomes a less disruptive activity that doesn't have to necessitate large-scale organisation change.

Providing the new service can deliver to the same contract as the outgoing service, other services or areas of the business shouldn't even need to be aware that the underlying software system has changed.

Read more on how we helped online retailer Surfdome to [evolve their retail monolith to microservices](https://www.madetech.com/resources/case-studies/surfdome-monolith-to-microservices).


## Modern Technology Continuously Delivered

A nod also needs to be made to how, and how often forward-facing retailers are pushing changes to their platforms.

Practising Continuous Delivery - the automation of the build, test, and deployment steps of software delivery has been the norm in modern businesses for the best part of a decade. This allows more frequent and more reliable changes to be made to production software systems.

Retailers such as [Etsy](https://www.infoq.com/news/2014/03/etsy-deploy-50-times-a-day) have lead the way with this approach, though we observe many established retailers in various stages of adoption of Continuous Delivery and wider systems and development lifecycle automation. Sainsbury's for example are particularly active in the [London Ansible scene](https://www.meetup.com/Ansible-London/).


## Where to Start

For retailers who are carrying the burden of legacy systems and services, it can be hard to see a route forward to a more modern platform without ripping out the foundations and starting afresh.

This is seldom a sensible choice when a business needs to continue trading in the short to mid-term, and seldom does the big bang replacement deliver the desired business value, or the promised technology nirvana.

In almost all cases, we would suggest adopting an evolutionary approach. Identifying a system, or subset of a system that is approaching the end of its useful life, and look to extract those responsibilites out to a new, single purpose service. Techniques such as [Anticorruption layers](http://wiki.c2.com/?AnticorruptionLayer) or the [Autonomous Bubble Pattern](http://dddcommunity.org/library/evans_2011_2/3) to allow new services to exist alongside elements of the legacy platform.

The evolutionary approach removes significant risk by focusing on a smaller area of the system as the candidate for replacement, allows uncertainty to be uncovered sooner, and delivers value back to the business by getting something working in to the hands of end users faster.
