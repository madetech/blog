IaaS vs. PaaS: what we've learned
=================================

We've been long-time proponents of PaaS, or Platform as a Service. We've also been long-time consumers of IaaS, or Infrastructure as a Service.

At its most simplistic, you could describe IaaS as renting something that closely resembles a server for a period of time. You could describe PaaS as altogether something more full-featured - a cohesive suite of tools on which to run and manage your (typically web) application.

Much of our leaning over the past three or four years has been towards AWS for IaaS, and Cloud Foundry for PaaS. Though we've variously trialled Rackspace Cloud, Heroku and Appfog.

In this post I'll compare our learnings on a number of key areas pertinent to both development and operations folk: performance, reliability, scalability and application management.


Performance
-----------

Day-to-day, you're unlikely to see significant difference between IaaS and PaaS for a typical application at runtime. That said, as PaaS is further away from the 'tin', in much the same way as comparing physical and virtualised hardware, you're going to see some loss.

Round 1: IaaS. But not by much.


Reliability
-----------

This should be an area in which PaaS excels, certainly if you believe the marketing hype.

If you're looking at reliability from an application management perspective, and by that, we mean the ability to detect unstable or misbehaving application instances and take corrective action, then PaaS does indeed provide some strong tooling around this.

However, if we're looking at the platform as a whole, we find PaaS to be more unrealiable than IaaS. Because of the increase in moving parts involved in a PaaS system, there are more components to fail, and subsequently, increased instances where intervention is required.

Round 2: IaaS.


Scalability
-----------

In this area PaaS offers some benefits over PaaS, though does fall short on autoscaling options.

In a typical PaaS setup, increasing or decreasing the number of application workers is no more complex than issuing a command. This can be particularly useful for predictable high traffic events, or for manually reacting moderately quickly to unexpected bursts in traffic.

IaaS offers little out of the box in terms of instance scale. Assuming your application servers are behind a load-balancer, you can add more instances and then deploy the latest version of your application to these instances to achieve the same outcome - though you're probably looking at 15 minutes over the 15 seconds for PaaS.

IaaS, and particularly the AWS platform, offers some strong tooling around autoscaling, though there's a heavy amount of customisation required to generate machine images for every release and to manually configure rules that trigger up- and down-scales.

Round 3: PaaS; though we'd like to see better autoscaling.


Application lifecycle management (ALM)
--------------------------------------

This is the area in which IaaS really doesn't stand a chance, the significant selling point of any PaaS platform.

If you go the IaaS route, you'll need to roll your own solution for managing applications, from provisioning infrastructure, deploying application changes and scaling application instances. Many quality tools exist in this space, but you're going to miss out on the turnkey access to them that PaaS provides.

Most (all?) PaaS platforms provide a uniform interface to perform common application management tasks. A particular selling point is the ease at which you can replicate entire environments. In simpler setups, you can expect to launch a clone of your entire production estate in a couple of minutes.

In addition, most PaaS ecosystems include a marketplace that can allow you to easily bind third party services such as cache services, proxies, mail relays and database services. We've found for small requirements, such as bolting a Redis queue backend on to an app - the ease, cost and removed maintenance overhead is significantly attractive in the PaaS world. Some more core services such as an application's primary database, we've found lacking in the PaaS marketplace and have fallen back on services such as Amazon RDS.

Round 4: PaaS. IaaS never really stood a chance.


IaaS or PaaS, then?
-------------------

By some cruel twist, we've demonstrated that IaaS is stronger in some areas and PaaS in others, which is really the reality of the situation.

From our experience, we'd have to recommend that for really mission critical applications, PaaS is still too immature with too many moving parts to be considered a viable option.

Where you're able to stomach a moderate level of risk, PaaS can offer significant agility in your ability to launch and manage new applications. Even if you're under good configuration management within your IaaS fleet, PaaS is likely to deliver you a runtime environment in a fraction of the time. For organisations with esoteric procurement cycles and manual infrastructure configuration, the leap forward is almost immeasurable.

