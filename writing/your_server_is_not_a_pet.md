Your server is not a pet
========================

You should treat your servers as cattle, not as pets. While we can't claim to have coined this catchphrase here at Made, it is certainly a philosophy that we subscribe to.

Pets are things you form a bond with, give a fluffy name, exhibit a unique personality, and are nurtured when they become sick. Cattle on the other hand are branded with an identifier, are near identical to one another, and if they become sick, you shoot them.

We view manual configuration of both servers and network infrastructure as an antipattern that should be avoided. The role of a sysadmin logging in to a server and making changes is A Bad Thing, and an activity that should be resigned to history.


Don't hand-rear your servers
----------------------------

There is a whole industry of configuration management tools that exist to allow you to provision servers in to a known good state quickly and repeatably. Ranging from the likes of [Chef](https://www.chef.io/) and [Ansible](http://www.ansible.com/home) which provide operating system-up configuration management, to [BOSH](https://github.com/cloudfoundry/bosh) and [Terraform](https://www.terraform.io/) that enable you to manage the network, servers, and everything beyond.

As soon as somebody logs in to a server and starts issuing commands to change the state of that server, its integrity has been compromised. You have no reliable way to get a server in to that state again and your ability to trust pre-production/production parity has now been removed. You've created a [snowflake](http://martinfowler.com/bliki/SnowflakeServer.html). 


Keep state where you can see it
-------------------------------

You should make moves to keep application state in very specific places within your herd. If you're talking about an average web application, this is probably going to mean data stored in your database and user uploaded content on some sort of filesystem. Unless a specific server role needs to permanently store data, do everything you can to avoid it.

For our money, there are a number of services available that make it someone else's responsibility to store and replicate this data, such as [Amazon RDS](http://aws.amazon.com/rds/), [Rackspace Cloud Databases](http://www.rackspace.co.uk/cloud/databases), [Amazon S3](http://aws.amazon.com/s3/) and [Rackspace Cloud Files](http://www.rackspace.co.uk/cloud/files).

If you really can't avoid storing application state on your own infrastructure, you'll need to be mindful of the additional data restore step needed when replacing nodes.


So what?
--------

So you've told your sysadmin to stop typing, invested in building a library of Chef recipes, and ensured your app is built to [Twelve-Factor](http://12factor.net/) principles. What now? 

We realise a number of significant benefits from adopting this approach to infrastructure management:

1. Scalability: scaling is now as easy as either reprovisioning a node on better hardware (vertical scaling), or provisioning a new node on similar hardware (horizontal scaling)

2. Disaster Recovery: replacing failed nodes requires nothing more than reprovisioning the failed instance (indeed, some tools such as BOSH can automatically orchestrate this for you)

3. Single source of truth for server configuration: If you want to understand how a server is configured, you can read the code that configures it. As you've checked this configuration in to source control, you've got a fully audited history of every change.

4. Reduced vendor lock-in: As you have the means to recreate your entire herd, usually in a matter of minutes, the barrier to moving to new infrastructure providers can be significantly reduced.

5. Ability to reproduce production-like environments: For running things such as performance tests or destructure security testing, spinning up a complete replica of the production environment for a short time, particularly when paired with a pay-per-hour infrastructure provider gives significant flexibility.


So what, next?
--------------

We see significant interest in tooling such as BOSH and Terraform. The likes of Chef, Ansible, Puppet and friends provide excellent tooling for managing your server configuration; though we still often see manual steps involved in provisioning in the underlying infrastructure and configuration of things like network interfaces.

Tools such as BOSH and Terraform either compliment or replace what is offered by these tools by taking management a step further - by interfacing direct with the underlying infrastructure. We're actively investigating Terraform as a means to document and manage our AWS fleet ongoing.
