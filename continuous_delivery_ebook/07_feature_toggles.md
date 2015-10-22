#More toggles, fewer branches 

###Feature Toggles
When practising Continuous Delivery, it's important that your application is deployable at all times. This can introduce some challenges, especially when you have features that span multiple builds, or bug fixes that need to get into production quickly. 

In this article, we're going to look at some of the techniques that we use to keep our applications deployable. We'll look at why branches (particularly long-lived ones) can be the kiss-of-death for a continuous integration project. Why techniques like feature toggles are useful, but should be used with caution. Why release toggles are frounded upon by Margi else, once we've completed the article. 

###Decoupling deployment and release
I'm sure we've all run into this problem before: You've got a set of changes which have been in development for weeks. For whatever reason, these can't be deployed through to production. Suddenly there's small bugfix that is urgently required and which need to be deployed right away. What do you do?

Well it's time to start looking at ways in which you can decouple the deployment and release of your code changes. 

If you had used a feature toggle and were able to enable / disable features, you could disable the offending feature and continue your continuous delivery practices Without this, you may have to perform a revert, implement the bug fix and then deploy this through your pipeline, before re-applying the bug fix to master. This is risky, potentially very complex and the sort of thing you really should be trying to avoid. 

###Small Releases
One of the first things we 

###Prevent long lived branches

###Branches go stale

###Branches create merge nightmares

###Feature flags a

#Feature Toggles
The basic idea behind feature files is to have a configuration file that defines a bunch of toggles for various features you have pending. The running application then uses these toggles in order to decide whether or not to show the new feature.

###Branching in code vs branching in source control
One of the criticisms of feature toggles is that they can introduce unnecessary code branches within your application. This is fair, as you're effectively putting features into conditionals statements and therefore increasing the cyclomatic complexity of your application. 

###Added test complexity
This also adds further complexity to things like your test suite, as you may need to test significantly more pathways through your application. 




##Dark launching
One of the approaches that we recommend is 'dark launching'. This involves deploying your application changes into production, but having them hidden to end users. At it's most simple, you can achieve this through hidden URLs or by not making a feature visible to all or a subset of users of your application.  