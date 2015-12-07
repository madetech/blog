

# Part II Technical Challenges with adopting CD

## Developers aren't ready

Truth be told, the majority of existing code bases aren't ready for Continuous Delivery.

Monolithic code base - not split into components

Moving to CD takes enormous amounts of discipline. Nowhere else is this more apparent that with your developers.

Not disciplined enough to check their work before commmitting
With new CD adptions this lack of discipline most commonly manifests itself, at least initially with an increase in errors/defects in production. A lot of this stems from a developers treating QA as a safety net, to catch their mistakes before they get there. In a CD setup, your QA funtion is much more than a final check of quality. Quality instead should be built into foeatures from the start, Testers should work with Developers from the very beginning of building a new feature,

No code reviews/pairing

<!-- Work 'given' to developers, rather than team self organising -->

## QA aren't ready

There is a general general priciple which states that the cost of fixing a defect increases exponentially the closer to production those bugs are discovered.
Your biggest protection against introducing defects in production is a robust automated test plan.

### Lack of, or lack of trust in automated tests

When deploying as regularly as a couple of times per day, even if only to a UAT environment, being reliant on a long-running manual test phase isn't feasible. If the application doesn't have automated test coverage, particularly for the most critical paths, your ability to deploy fast is going to be significantly compromised.

Almost as detrimental can be a test suite that you don't trust. If the suite is known to suffer from flickers (where a test can seem to randomly pass and fail between different test runs), or where the tests aren't of sufficient quality to be providing meaningful coverage, the confidence in the test suite can be eroded, increasing the reliance on manual testing.

### Caveat that we don't have a QA team at Made

QA testing code in staging/continuous - should be involved much earlier ideally writing tests before code is written

### Long running automated test suite

A long running test suite can pose challenges in your ability to move quickly. If you need to wait more than 10 minutes or so for feedback (and we've seen cases of close to an hour!), not only is your workflow is likely to be impacted, but subsequently, your ability to deploy fast is going to be compromised - because every change needs to be pushed through the pipeline, starting at the buld step.

This can be particularly tough in cases where you have a business critical change or fix that needs to navigate the pipeline fast.

### No smoke tests

Too often smoke tests are overlooked. Without them, there's generally a period post-deployment where critical pathways need to be manually verified, increasing the human burden required in deploy changes.

Where there's an integration suite to keep confidence high that change hasn't broken pre-existing features at a code level, smoke tests provide the same confidence that the critical application pathways are working as expected post-deployment.



## ops aren't ready

High Availbility and Continuous Delivery are more closely aligned than most people realise. If you were to lose all your hardware tomorrow - how quickly could you get everything back online?

Does each server have its own custom configuration (cf Your server is not a pet). How automated is your recovery plan? In a pure CD environment each deployment is treated the same as a complete hardware failure, we tear everything down and start again (with the caveats that our Database is probably a special case, and in a deployment, we'd spin up our new estate /prior/ to tearing down the old!)

If you have a multitude of snowflake servers, and little configuration committed to source control, you're going to have a hard time moving to CD.

Long build times are also a factor here, if a deployment currently takes 8 hours regardless of whether this is an automatic or manual proess, that's an extra 8 hours added to each and every feature you build in a CD environment. If you want your team to build 4 features a week, that only leaves 2 hours to plan, build and test each feature!


### Frequent rollbacks

Rolling back (or forwards) production deployments often is a smell that some earlier parts of the pipeline aren't as optimised as they could be.

If significant issues are finding their way in to production undetected, you're probably not baking enough quality in to your process from the outset. If the production deployment behaves differently to deployments to pre-production environments, you don't have sufficient parity in your environments.

We'd recommend tracking your deployment success rate to as a good measure of the overall quality of your delivery pipeline.


## External parties aren't ready

Seldom is a development team entirely self contained. At some point you will have some sort of reliance on an external team.

Particularly where an external team isn't able to work using a similarly compatible delivery method, your team's ability to move fast and release often can easily be compromised. Where possible, we try to isolate high-cadence teams from any external factors that may slow down releases, making use of techniques such as mocking to allow early integration against unknown interfaces, to feature toggling to allow features to be enabled in production when a third party's development schedule has caught up.


## conclusion


