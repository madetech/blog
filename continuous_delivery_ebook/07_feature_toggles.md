#More toggles, fewer branches 

When practising Continuous Delivery, it's important that your application is deployable at all times. This can introduce some challenges, especially when you have features that span multiple builds, or bug fixes that need to get into production quickly. 

In this article, we're going to look at some of the techniques that we use to keep our applications deployable. We'll look at why branches (particularly long-lived ones) can be the kiss-of-death for a continuous integration project. Why techniques like feature toggles are useful, but should be used with caution. And why you should focus on actually delivering small incremental changes to production, as this will make everything much easier. 

###Decoupling deployment and release
I'm sure we've all run into this problem before: You've got a set of changes which have been in development for weeks. For whatever reason, these can't be deployed through to production. Suddenly there's small bugfix that is urgently required and which need to be deployed right away. What do you do?

Well it's time to start looking at ways in which you can decouple the deployment and release of your code changes. 

If you had used feature toggles and were able to enable / disable features, you could disable the offending feature and continue your continuous delivery practices. Without this, you're probably going to need to perform a revert, implement the bug fix and then deploy this through your pipeline, before re-applying the bug fix to master. This is risky, potentially complex, and the sort of thing you really should be trying to avoid. 

###Prevent long lived branches
In this scenario, some people would advocate developing the feature in its own branch and merging this back into master once the feature is complete. We have found this creates an additional set of challenges and complexity and goes against many of the principles of continuous integration (where you should be integrating into a shared repository multiple times per day). 

####Branches create merge nightmares
If you've ever tried to merge a long lived branch, which contains a complex set of changes into a master branch that is under active development, then you probably know how much of a nightmare complex merges can become. You've probably experienced that sick feeling in the pit of your stomach when confronted with dozens or even hundreds of merge conflicts needing to be addressed. 

####Feature branches and pull requests
The one type of branch that we would use is a short-lived feature branch, as part of a pull request type workflow. My colleague Fareed has [written an article about this and how we use these for pull requests based workflows.](https://www.madetech.com/blog/pull-requests-and-continuous-integration)

#Feature Toggles
Moving onto feature toggles. The basic idea behind them, is that you to have a configuration system that allows you to toggles features on or off depending on some factors, such as environment, user profile or market. The running application then uses these toggles to decide whether or not to show the feature.

The actual implementation can take many forms. At its simplest, you'll have a static configuration file within your application, which you'll need to deploy to production for the toggle changes to take affect. Some companies use more complex feature toggling systems, to allow runtime feature toggling via an admin interfaces or for toggling features within a canary build.

##Benefits of feature toggles
There are a number of benefits to feature toggles, such as the ability to gradually roll out new features, properly decouple the deployment of code and the release, provide developers will a nice framework for developent. 

###Branching in code vs branching in source control
One of the criticisms of feature toggles is that they can introduce unnecessary code branching into your application. You're effectively putting features into conditionals and therefore increasing the cyclomatic complexity of your application. 

This code branching needs to be managed or you're fairly quickly going to start accruing technical debt in your application. Jim Bird wrote an interesting article on this and [described some techniques](http://swreflections.blogspot.co.uk/2014/08/feature-toggles-are-one-of-worst-kinds.html) that he would recommend using to prevent the accrual of too much debt in your application. 

###Added test complexity
Another area in which you need to consider the impact of feature toggles, is within your test suite. There is a significant overhead to testing all combinations, and frankly, it would be difficult to justify the impact this would have on the performance of your test suite. 

Martin Fowler recommends having tests which cover:

* All the toggles on that are expected to be on in the next release
* All toggles on

###Small incremental releases
You should try and break features into small incremental chunks, which are releasable. By doing this, you're minimising risk and more quickly realising value from your development effort. 

##Dark launching
One of the approaches that we recommend is 'dark launching'. This involves deploying your application changes into production, but having them hidden to end users. At it's most simple, you can achieve this through hidden URLs or by not making a feature visible to all or a subset of users of your application.  

###Conclusion
As a developer, it's your responsibility to manage application complexity. We would recommend you try and adopt a 'small and incremental' mindset as your default course-of-action, as this has the lowest complexity overhead. 

Only when this becomes impossible to achieve should you look towards feature toggles, as they will add complexity and ideally you want to minimise this as much as possible. 