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

### Expecting the unexpected

  When practicing contious delivery it is not to say that that you are going to introduce bugs into your code.
  The key benefit to practicing continous delivery is that it is easier to recover and identify what went wrong.

  You and your co-workers need to understand that bad things do happen and need to have a good backup plan for dealing with them quickly.

  If a bad commit were to be introduced into production, you need to be able to correct this in the least amount of time possible.

  This usually means rolling forward with another commit through your pipeline to address it.

  Netflix introduced the Chaos Monkey which does destructive things.

### Deployment Software

  Abstract and simplify your deployment process.  You can use something as simple as a bash script but as this grows in complexity it is usually best
  to test up a continuous deployment environment like Jenkins.

  Some chat bots can even be programmed to do the deployments for you from your chat application.

  In order to minimize human error you must encapsulate your entire deployment process in as few steps as possible.
  The perfect optimal number of steps being 1.  By doing this you have moved your deployments one step closer from nerve racking to being boring.

  Blue / Green deploys are also a nice safety net for switching back to the last version of the production application.
  Basically you have two pools of application server instances running with a loadbalancer serving traffic to just one a time.

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
