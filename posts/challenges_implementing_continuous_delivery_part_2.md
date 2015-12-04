

# Part II Technical Challenges with adopting CD

## developers aren't ready

Truth be told a vast proportian of code bases aren't ready for continuous delievery
Monolithic code base - not split into components

Moving to CD takes enormous amounts of discipline. Nowhere else is this more apparent that with your developers.

Not disciplined enough to check their work before commmitting
With new CD adoptions this lack of discipline most commonly manifests itself, at least initially with an increase in errors/defects in production. A lot of this stems from a developers treating QA as a safety net, to catch their mistakes before they get there. In a CD setup, your QA funtion is much more than a final check of quality. Quality instead should be built into features from the start, Testers should work with Developers from the very beginning of building a new feature, 

No code reviews/pairing

<!-- Work 'given' to developers, rather than team self organising -->

## QA aren't ready

There is a general general priciple which states that the cost of fixing a defect increases exponentially the closer to production those bugs are discovered. 
Your biggest protection against introducing defects in production is a rubust automated test plan. 

Lack of, or lack of trust in automated tests

Caveat that we don't have a QA team at Made

QA testing code in staging/continuous - should be involved much earlier ideally writing tests before code is written

Long running automated test suite

No smoke tests/integration tests

## ops aren't ready

High Availbility and Continuous Delivery are more closely aligned than most people realise. If you were to lose all your hardware tomorrow - how quickly could you get everything back online?

Does each server have its own custom configuration (cf Your server is not a pet). How automated is your recovery plan? In a pure CD environment each deployment is treated the same as a complete hardware failure, we tear everything down and start again (with the caveats that our Database is probably a special case, and in a deployment, we'd spin up our new estate /prior/ to tearing down the old!)

If you have a multitude of snowflake servers, and little configuration committed to source control, you're going to have a hard time moving to CD.

Long build times are also a factor here, if a deployment currently takes 8 hours regardless of whether this is an automatic or manual proess, that's an extra 8 hours added to each and every feature you build in a CD environment. If you want your team to build 4 features a week, that only leaves 2 hours to plan, build and test each feature!

frequent rollbacks
Do you track deployment success rate?

## external parties aren't ready

Seldom is a development team entirely self contained, at some point you will have some sort of reliance on an external team, this can be 
external parties on long feedback/change cycles


## conclusion


