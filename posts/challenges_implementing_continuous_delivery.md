## Intro

## Culture/organisation isn't ready

Adopting CD for a single team is tough, adopting CD across multiple teams is infintely more complex. In a 'traditional' software setup, with separate product, architecture, development, Quality Control and Operations teams, a move to continuous likely impossible unless you have exceptional levels of communication between all these teams. Such a team structure almost invariably leads to a 'throwing it over the wall' mentality though. Where each team does its job, before throwing the feature to the next team in the pipeline thus:

[Product Team] => [Architecture] => [Software devlopment] => [QA] => [Ops]
This is a pipeline of sorts, but upone closer inspection it doesn't appear especially fault tolerant. The biggest issue is how to ensure that each of the five teams are working at the exact same rate? If the Product Team are defining features faster than they can be arcitcted, then we have a bottleneck. Items are sitting idle in the architecture queue, waiting for someone to pick them up. Over time this leads to a massive Architecture backlog which becomes impossible to prioritise.

The opposite problem is equally likely, lets imagine the development team can build features faster than the Architects can specifiy them, and also faster than QA can test them. Well now there's a very real chance that your developers will run out of stuff to do!

[Diagram showing pipes with different rates of flow:]

|---------|--------------|--------------|         |------------|
> Product > Architecture >              |---------| Deployment |
|         |--------------|  Development > Testing >            >
|---------|              |              |---------|------------|
                         |--------------|


In such a system water will flow at a rate of the thinnest pipe. You can't mitigate this by expanding a single pipe, as that will just move the bottle neck elsewhere. Bottlenecks are a disfunction and they'll lead to frutration of the team, and a culture of blaming others for slowing the whole down.

Fixing the problem needs a complete rework of the plumbing, rather than each team being responsible for their part of the pipe, the team as a whole need to be responsible for the entire throughput of the system, this can only happen when the team is equally responsible for the whole:

|--------------|-----------------------| 
>  Input pipe  >                       | 
|--------------|  Team Responsibility  |---------------|
               |                       >  Output pipe  >
               |-----------------------|---------------|

Note that any team, regardless of scope will have its inputs and outputs, the adoption of CD is fundamentally about teaching teams to group up and share their respective connections. rather than rebuilding a delivery pipeline overnight, its usual to gradually grow the scope of a teams remit piece by piece. You might start for example by joing the Dev & Architecture functions, and sharing their upstream connection with Product, and downstream with QA. To continue with the metaphor, you replace 2 pipes with one, and do this incrementally until the whoel team is respnsible for its inputs and outputs as a whole. Once these 5 are joined there's nothing to stop you widening the principle further!

Another key mindset that is important to change when moving a business over to Continuous delivery, is how to measure success/progress. Even commonly practiced Agile methodologies start to fall down when faced with genuine continuous delivery. Take Scrum as one example, what value does a Sprint Demo have in such an environment? In a two week sprint we'll have close to a dozen features in production by the end so is there value sitting stakeholders down and running through features they've likely already seen? How does measuring a teams velocity over two weeks help us figure out where bottlenecks are so that we can improve? It's likely in such an environment that average cycle time - i.e. how long it takes to go from inception to production - will be much more meaningful.

Delivering value to customers is the ultimate goal of any software project, actually measuring this is generally quite difficult with a large change set though. Once you are delivering atomic units of value in a continuous delivery fashion it becomes much easier to measure this. By tracking key performance metrics from build to build you can easily see which builds had the biggest impact on customer value. Combine this with cycle time and you have two very powerful tools for determining the most valuable work for the team to focus on.

<!-- Where a lot of companies struggle is in valuing of individuals over the team as a whole. That is the output of the team is controlled by one or two ey people, whether that is business stakeholders, or a lead developer, it's important t -->
Broadly speaking, there are two kinds of deadlines - soft deadlines, and hard deadlines. I define them as such

* Hard deadlines - a fixed date in the calendar, where something must be delivered otherwise significant business harm will result. e.g. We must complete our tax return by the end of the year otherwise we will pay heavy fines.
* Soft deadlines - these are everything else. Most deadlines should be soft deadlines.

How your business treats deadlines is a useful indicator of how successfully they might adopt continuous delivery. The following are all 'smells' which are going to make CD difficult:
 * Soft deadlines frequently masquerade as hard deadlines: i.e. we need this feature by this date because this is when we've promised it to customers.
 * Teams have no control over their soft deadlines
 * Teams are heavily punished for failing to meet soft deadlines

It's common for concepts such as technical debt & code health/quality are alien concepts outside of your immediate tech team. Which is odd, as they have perhaps the biggest impact over speed of delivery - or as we defined it above, cycle time. Exposing these metrics as loudly as you can is a great way to encourage the business to take more of an interest in them. This also gives a yardstick to measure the success of initiatives to improve these metrics. It's much easier to make the business care about these metrics when faced with concrete data such as "We spent half a sprint and increased test coverage in this section of our application by 50%, and sped up build times by 15% - this has removed a day from our mean cycle time for this component meaning we can get new features in front of customers 10-20% faster."

Focussing on the wrong stuff too much time on new stuff vs 

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

## customers aren't ready

Customers complain when things change often

don't understand how software is written

don't understand incremental change

not consulted about upcoming changes

no comms channel between tech & customers

## conclusion

