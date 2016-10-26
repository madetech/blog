# Giving teams an environment where everyone can deploy safely any time

## What do we mean by deploying safely at any time

  We believe that all developers should be allowed to deploy at any time.  Both developers and management find this scary since it makes traditional
  release management and QA very hard.  We have found that empowering developers to own this responsibility allows you to ship software much faster
  whilst maintaining or even improving the safety of the traditional processes.

  Anyone who introduces a new feature should be allowed to push it into production and should take responsibility for that change.
  This means that an engineer will not only make a change to the code but deploy it, ensure that it functions as expected in production and even be in
  touch with the stakeholders about it.  Should anything go wrong, they are responsible for fixing it.

## Why everyone should deploy their own changes

  The biggest benefit when empowering teams to deploy safely at any time is that your deployments become faster and less riskier over time. Removing overheads such as QA processes means that we can make changes quickly. By making more frequent changes they will naturally be smaller. If our deployments are smaller they will be easier to test and easier to fix in the case of any issues. Deployments become mundane.

  Over time your team will become better at testing their own changes and fixing issues when they arise. When a developer releases a change they will learn to become responsible for testing and monitoring it. This creates a proactive culture where developers can quickly react to problems often allowing them to spot defects before many users encounter them.

  Not only do the business and customers benefit from more frequent changes but we've found empowered developers are happier developers. By being responsible for a change, from start to finish, developers will feel a sense of pride and ownership over their work. We've found more traditional release strategies lead to developers passing responsibility onto QA or the deployment team, simply throwing their work over the fence. When developers own their changes, they will put care into their work.

  // Could talk about less staff being involved therefore less of a distraction, less of a cost to the business

## How to provide a safe deployment environment
  From our experiences we have found the following 6 steps to greatly improve the way in which software is deployed.

    - Create a safe environment where it is ok to fail
    - Make deployments easier by automating them
    - Production like environment for testing
    - Deployment frequency
    - Transparency
    - Monitoring
    - Rolling forwards and backwards

### Create a safe environment where it is ok to fail

  It is rare in software engineering that changes are perfect first time round, we have found that optimising for fixing failures quickly provides
  more value than getting things right the first time round.  In order to benefit from deploying faster, you first need a culture where failure is ok.

  If a bad commit were to be introduced into production, you need to be able to correct this as quickly as possible.

  - Fast recovery
  - Redundancy
  - Don't punish failure, reward recovery
  - Transparency with stakeholders

### Make deployments easier by automating them

  Humans aren't great at repeating processes, and let's face it it can be boring too.

  A typical deployment will include building, testing and releasing it to the public.

  The risk of errors can be reduced by automating the steps of a deployment.
  It should be repeatable and easy to understand, this can range from a simple script on the developers computer or a hosted continuous integration service.

  This will reduce the pressure of introducing a defect into the system as a rollback can happen in a few seconds.

### Production like environment for testing

  You should have a staging environment with data that mirrors production.
  This data can be made repeatable by managing it with seeds.

### Deployment frequency
  Keeping your deploys frequent means that the code being deployed out will be small enough to reason about in isolation.
  The more frequent the deploys, the less risk each of them carries.

### Transparency
  Broadcast deploys happening on the various environments on your chat so that everyone can see when one has occured.
  You shouldn't need to ask whether you can do a production deploy as the pipeline should be clear.

  Even your stakeholders should be subscribed to this channel to see when this happens.
### Monitoring
  You need good monitoring in your application to get an idea of the error frequency and performance.
  After a deploy to production, the developer who pushed it up should keep an eye on the monitoring to see if any obvious defects had been introduced.
### Roll forwards, roll backwards
  If you deploy frequently and monitor the system after each deploy, you should have a pretty clear picture on which deploy had adverse effects on the
  system.  Knowing this, it should be trivial to track down the commit and fix it.  Hopefully you practice

  This should be the last resort for any fix needed to get into production.  You should always prefer to roll forward instead of back.

  Blue / Green deploys are also a nice safety net for switching back to the last version of the production application.
  Basically you have two pools of application server instances running with a loadbalancer serving traffic to just one a time.
