# Giving teams an environment where everyone can deploy safely any time

## What do we mean by deploying safely at any time

  We believe that all developers should be allowed to deploy at any time.  Both developers and management find this scary since it makes traditional
  release management and QA very hard.  We have found that empowering developers to own this responsibility allows you to ship software much faster
  whilst maintaining or even improving the safety of the traditional processes.

  Anyone who introduces a new feature should be allowed to push it into production and should take responsibility for that change.
  This means that an engineer will not only make a change to the code but deploy it, ensure that it functions as expected in production and even be in
  touch with the stakeholders about it.  Should anything go wrong, they are responsible for fixing it.

  Having another developer look over the changes could also help spot any bugs.  Ideally someone who has not touched the code, and simply tests the
  system like a user would.

## Why everyone should deploy their own changes

  The biggest benefit when empowering teams to deploy safely at any time is that your deployments become faster and less risky over time. Removing overheads such as QA processes means that we can make changes quickly. By making more frequent changes they will naturally be smaller. If our deployments are smaller they will be easier to test and easier to fix in the case of any issues. Deployments become mundane.

  Over time your team will become better at testing their own changes and fixing issues when they arise. When a developer releases a change they will learn to become responsible for testing and monitoring it. This creates a proactive culture where developers can quickly react to problems often allowing them to spot defects before many users encounter them.

  Not only do the business and customers benefit from more frequent releases but we've found empowered developers are happier developers. By being responsible for a change, from start to finish, developers will feel a sense of pride and ownership over their work. We've found more traditional release strategies lead to developers passing responsibility onto QA or the deployment teams, simply throwing their work over the fence. When developers own their changes, they will put care into their work.

  One common argument that may come up is that developers will be swapping depth of knowlege in a particular field for breadth which spans many fields.
  While this is a reasonable concern we have found that this is not as drastic as it may seem.

  Building up experience is rewarding and what most passionate developers strive for.  However, a developer could have 10 years of experience but it
  could be 10 x 1 year experience doing the same thing.  By delivering features end to end you are often forced to think about the problem from a different angle.  This may impact both the volume the type of code that is written by the developer.

## How to provide a safe deployment environment

  From our experiences we have found the following 6 steps to greatly improve the way in which software is deployed.
  These can be expanded on but having these in place will greatly benefit your releases.

    - Create a safe environment where it is ok to fail
    - Make deployments easier by automating them
    - Production like environment for testing
    - Deployment frequency
    - Transparency
    - Monitoring
    - Rolling forwards and backwards

### Create a safe environment where it is ok to fail

  It is rare in software engineering that changes are perfect first time round, we have found that optimising for fixing failures quickly provides
  more value than getting things right the first time round. In order to benefit from deploying faster, you first need a culture where failure is ok.

  If a bad commit were to be introduced into production, you need to be able to correct this as quickly as possible.

  - Fast recovery
    Your code will not reach production unless it passes all the automated tests, so having a fast test suite is a requirement here.
    You will want to get a new commit out and through the build pipeline as quickly as possible to address the issue that was introduced.
    Ideally you can spot and correct this issue before the users or the stakeholders even know it's there.

  - Redundancy
    It is important to keep multiple backups of your data, hopefully you will never have to use it but it can be disasterous to not have it.

  - Don't punish failure, reward recovery
    Everyone makes mistakes, and it is an important part of learning.  That's not to say that you can let your guard down, you should still test every
    feature as much as possible.

    When you have a friendly environment for people to work in, they will produce better work.

  - Transparency with stakeholders
    Never hide the fact that defects made it to production, it might even facilitate healthy conversations about why this happened in the first place.
    Perhaps some refactoring is needed.

### Make deployments easier by automating them

  Humans aren't great at repeating processes, and let's face it it can be boring too.

  A typical deployment will include building, testing and releasing the software to the public.

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
  After any deploy to production, the developer who pushed it up should keep an eye on the monitoring to see if any defects had been introduced.

  It gives you information on how users are interacting with the new feature which usually yields more valuable information than when you were testing on your own.

  Since the nature of change does carry some risk the goal is to spot potential defects before anyone else does.
  Modern tools allow you to set up alerts when certain thresholds are exceeded.  You can get a pretty accurate overview of the error rate and
  performance.

### Roll forwards, roll backwards

  If you deploy frequently and monitor the system after each deploy, you should have a pretty clear picture on which deploy had adverse effects on the
  system.  Knowing this, it should be trivial to track down the commit and fix it.  Hopefully you practice TDD and introducing bugs is a rare
  occurrence.

  Rolling backwards should be the last resort for any fix needed to get into production.  You should always prefer to roll forward instead of back.

  If you have a good understanding of the change that affected the live system, you will be able to zone in on it and fix it.

  Blue / Green deploys are also a nice safety net for switching back to the last version of the production application.
  With this technique you have two pools of application server instances running with a loadbalancer serving traffic to just one of them at a time.

  If the bug that was introduced is so severe that there is no way to roll forward with a fix, you should be able to fall back to the last known good
  version with the click of a button. This should be a easy to do and should be a step in your deployment pipeline.
