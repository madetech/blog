

# Part II: Technical Challenges with adopting CD

I spoke last time about the organisational challenges of adopting CD last time. One of the key takeaways was the importance of blurring the boundaries between teams in order to facilitate better adoption. This time around I wanted to zoom in a bit and focus specifically on the challenges faces by specific parts of the pipeline. NB Depending on how far through adoption you likely no longer have dedicated teams for each of these functions, though the problems outlined here can still exist and derail any team

Unless your codebase has been written with CD in mind, or is very new, then it's very likely your first headache will be getting it ready to be built and deployed many times per day. In practice theres anumber of obstacles to this

##Automated tests

When deploying as regularly as a couple of times per day, even to a UAT environment, being reliant on a manual test phase just isn't feasible. If the application doesn't have automated tests, particularly for the most critical paths, your ability to deploy regularly is going to be significantly compromised.

Even if you have automated most of your tests, almost as detrimrental is a test suite that you don't trust. If you frequently suffer from flickering tests (where a test can seem to randomly pass and fail between different test runs); or simply where the tests aren't of sufficient quality to be providing meaningful coverage, the confidence in the test suite can be eroded, increasing the reliance on manual testing and thus slowing down your deployment pipeline.

The final big testing headaache is a long running test suite can pose challenges in your ability to move quickly. If you need to wait more than 10 minutes or so for feedback (and we've seen cases of close to an hour!), not only is your workflow is likely to be impacted, but subsequently, your ability to deploy fast is going to be compromised - because every change needs to be pushed through the pipeline, starting at the build step.

### Caveat that we don't have a QA team at Made
QA should build use cases with developers before any code is written
QA testing code in staging/continuous - should be involved much earlier ideally writing tests before code is written

##No code reviews/pairing
valuing specialism over generalism siloed knowledge etc,


##Poor code quality:
 toggling WIP features off in production can lead to code duplication / messy ‘toggle’ statements inline temporarily


##Monlithic architecture

##Long build times
Long build times are also a factor here, if a deployment currently takes 8 hours regardless of whether this is an automatic or manual proess, that's an extra 8 hours added to each and every feature you build in a CD environment. If you want your team to build 4 features a week, that only leaves 2 hours to plan, build and test each feature!

## automated deployments servers as code

Does each server have its own custom configuration (cf Your server is not a pet). How automated is your recovery plan? In a pure CD environment each deployment is treated the same as a complete hardware failure, we tear everything down and start again (with the caveats that our Database is probably a special case, and in a deployment, we'd spin up our new estate /prior/ to tearing down the old!)

If you have a multitude of snowflake servers, and little configuration committed to source control, you're going to have a hard time moving to CD.

### Frequent rollbacks

Rolling back (or forwards) production deployments often is a smell that some earlier parts of the pipeline aren't as optimised as they could be.

If significant issues are finding their way in to production undetected, you're probably not baking enough quality in to your process from the outset. If the production deployment behaves differently to deployments to pre-production environments, you don't have sufficient parity in your environments.

We'd recommend tracking your deployment success rate to as a good measure of the overall quality of your delivery pipeline.

##Over-reliance on brittle third-party dependencies
Seldom is a development team entirely self contained. At some point you will have some sort of reliance on an external team.

Particularly where an external team isn't able to work using a similarly compatible delivery method, your team's ability to move fast and release often can easily be compromised. Where possible, we try to isolate high-cadence teams from any external factors that may slow down releases, making use of techniques such as mocking to allow early integration against unknown interfaces, to feature toggling to allow features to be enabled in production when a third party's development schedule has caught up.

Too often smoke tests are overlooked. Without them, there's generally a period post-deployment where critical pathways need to be manually verified, increasing the human burden required in deploy changes.

Where there's an integration suite to keep confidence high that change hasn't broken pre-existing features at a code level, smoke tests provide the same confidence that the critical application pathways are working as expected post-deployment.

errors and defects rate in production. A lot of this stems from a developers treating QA as a safety net, to catch their mistakes before they get there. In a CD setup, your QA function is much more than a final check of quality. Quality instead should be built into features from the start. Testers should work hand-in-hand with Developers during the delivery of a feature to ensure it can be verified as soon as it hits the pipeline.


## conclusion
#measure and break down 'time to production'
#deployment success rate
#error/defect rate
Long build times are also a factor here, if a deployment currently takes 8 hours regardless of whether this is an automatic or manual proess, that's an extra 8 hours added to each and every feature you build in a CD environment. If you want your team to build 4 features a week, that only leaves 2 hours to plan, build and test each feature!
m

