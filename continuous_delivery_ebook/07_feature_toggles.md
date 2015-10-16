#Feature Toggles

###Introduction
When practicing Continuous Delivery, it's important that your master branch is deployable at all times. This can introduce some challenges when you have features that requires weeks or even months of development. 

You'll often end up with some code that is working but is not ready for end-users. When this happens, you'll have blocked your Continuous Delivery pipeline and will be preventing production deploys. In this article, we're going to look at some of the practices that can be used to circumvent this and ensure you keep your pipeline clear and 

###Decoupling deployment and release
The first thing you need to do is decouple the deployment and the release of the code changes. When we talk about deployments, we are referring to the code being in the production environment, but not necessarily run or executed. When we refer to a release, we're talking about end users (or a subset of users) being able to use a feature and the code actual executing. 

There are a number of reasons why decoupling these is important. To start with, it reduces your risk. Deploying code often involves complex things like database migrations, XXX and XXX. If you can separate these from 

##Dark launching
One of the approaches that we advocate is called a 'Dark Launch'. 

* Dark launching
* Phased rollouts
* Branching
** Prevent long lived branches
** Branching in code vs branching in source control


