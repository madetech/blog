# Part II: Technical Challenges with adopting Continuous Delivery

I spoke [last time](https://www.madetech.com/blog/continuous-delivery-organisational-challenges) about the organisational challenges of adopting Continuous Delivery. One of the key takeaways was the importance of blurring the boundaries between team ownership in order to facilitate better adoption. This time around I wanted to zoom in a bit and focus specifically on the challenges faces by specific parts of the pipeline. Depending on how far through adoption you likely no longer have dedicated teams for each of these functions, though the problems outlined here can still exist and derail even the most cross functional of teams.

Most applications, unless specifically developed with Continuous Delivery principles in mind, are a long way away from being built and deployed many times per day - a core tenet of Continuous Delivery. This is generally the first issue teams should tackle and there are many components to it.

## Automated testing

If you aspire to deploy code to production multiple times per day, or even to a UAT environment, being reliant on a manual test phase is impractical. If the application doesn't have automated tests, particularly for the most critical paths, your ability to deploy a working application regularly is going to be significantly compromised.

Even if you have automated most of your tests, it's also important to consider the reliability of your tests. One symptom of this are frequent test 'flickers' (where the same test seems to pass or fail randomly between different test runs); another is where your tests aren't of sufficient quality to provide meaningful coverage across the breadth of you application. These both contribute to a gradual erosion of trust in your own tests, and over time an increase in manual test steps. The end result being a much slower (and more manual) deployment pipeline than necessary.

The final big testing headache is a long running test suite. If you need to wait more than 10 minutes or so for feedback (and we've seen cases of close to an hour!), not only is your workflow is likely to be impacted, but subsequently, your ability to deploy fast is going to be compromised - because every change needs to be pushed through the pipeline, starting at the build step.

Automated testing in the absence of incredible amounts of hardware is a trade off. For an application of any meaningful size, having a test suite which covers 100% of your application, whilst also running in a few minutes isn't a realistic goal. It's important to analyze your test suite to ensure it's delivering you the most possible value, especially for the longer running tests. 

My final word on testing is to trust your tests. I've worked with teams who had great automated test coverage, but after a deployment the team insisted on testing user journeys manually. Some call this superstition, I call it madness! Why spend all that time writing tests if you're going to ignore what they tell you?

##Automated deployments

Long build times are a huge blocker to Continuous Delivery adoption. If your deployment currently takes 8 hours, then it's obviously impractical to do this multiple times per day! Considered another way, your cycle time per feature is 8 hours longer than it needs to be. In order to build 4 features per week and deploy them individually (at Made we strive for 4 features per day), leaves 2 hours to build and test each feature - in other words, it's not going to happen.

Are your servers [cattle or pets?](https://www.madetech.com/blog/your-server-is-not-a-pet). Much as we like to think every deploy is safe, you can't control everything and some deploys are just going to fail no matter what. This risk is compounded when you deployment methodology is to deploy sequentially to the same infrastructure. When a bad deploy happens your infrastructure can end up in a weird state and rather than trying to unpick everything it's far easier and quicker to blow it all away and start again. This is only possible with automated build scripts, and when all you configuration exists entirely within source control.

A canary server is a great way to detect issues early in a deployment. The idea behind these is to have a single instance running the new version of the application and gradually introduce it to live traffic. By watching error rates and tracking key consumer metrics (using automated tools of course) you can quickly flag problems which might prompt you to pull out of a deploy, or even fail automatically. In practice this is much easier than having to roll back a whole deployment.

## Over-reliance on brittle third-party dependencies

Seldom is a development team entirely self contained. At some point you will have some sort of reliance on an external team.

Particularly where an external team isn't able to work using a rapid delivery method, your team's ability to move fast and release often can easily be compromised. Where possible, we try to isolate high-cadence teams from any external factors that may slow down releases. We use techniques such as mocking and API integration tests, to define the contract between our application and external dependencies. 

Such tests become not only the documentation for the APIs, but also notify us if and when a third party changes their integration, so we can quickly respond. We usually deploy these changes behind a [feature toggle](https://www.madetech.com/blog/continuous-delivery-feature-toggles), so we can deploy the changes to production and move onto the next. Once the third party has caught up, as long as the integration tests are all green, turning on the new feature then just requires a configuration change within the application.

## Clean up after yourself

Too often Continuous Delivery is seen as an excuse to make rash decisions and never come back to clean them up later. This is something we're all guilty of to some extent. Things like:
 * Didn't address a couple of the comments from code review because we had to get the feature out today
 * Duplicate an existing class and modify it slightly, rather then refactor the existing code.
 * Deployed a feature without adequate tests.
 * Found an edge case but didn't have time to fix it.
 * Activated a feature via a feature toggle, but never removing the code for the feature toggle which is no longer needed.

I'm not saying the rationalisation of any of these things are good, but in a rapidly evolving code base technical debt can spiral out of control fast. It's important to realise that building and deploying features rapidly, does not mean doing things half-arsed. There are times when cutting a corner is necessary, my rule of thumb is that this is ok only if you have a good reason (which you are comfortable justifying to others) and a plan to make it good within the next few days.

## Conclusion

Going from a cycle time of a few days to a few hours isn't going to happen overnight and deciding what to focus on first is an important step on your Continuous Delivery journey. Analysing cycle time of features - the time from when an idea was conceived to when it was successfully deployed - will help you quickly identify bottlenecks in your process. If 50% of cycle time is spent on deploying features, it's fair to say there's real value to be had speeding that up. Likewise, if there's idle time waiting for stakeholders to feedback on requirements, then whilst there's value in speeding up automated tests, there's probably more value ensuring your engineers are getting everything the need from the rest of the business.
