## Intro

## Culture/organisation isn't ready

Adopting CD for a single team is tough, adopting CD across multiple teams is infintely more complex. In a 'traditional' software setup, with separate product, architecture, development, Quality Control and Operations teams, a move to continuous likely impossible unless you have exceptional levels of communication between all these teams. Such a team structure almost invariably leads to a 'throwing it over the wall' mentality though. Where each team does its job, before throwing the feature to the next team in the pipeline thus:

[Product Team] => [Architecture] => [Software devlopment] => [QA] => [Ops]
This is a pipeline of sorts, but upone closer inspection it doesn't appear especially fault tolerant. The biggest issue is how to ensure that each of the five teams are working at the exact same rate? If the Product Team are defining features faster than they can be arcitcted, then we have a bottleneck. Items are sitting idle in the architecture queue, waiting for someone to pick them up. Over time this leads to a massive Architecture backlog which becomes impossible to prioritise.

The opposite problem is equally likely, lets imagine the development team can build features faster than the Architects can specifiy them, and also faster than QA can test them. Well now there's a very real chance that your developers will run out of stuff to do!

[Diagram showing pipes with different rates of flow:]

|---------|--------------|--------------|         |------------|
| Product | Architecture |              |---------| Deployment |
|         |--------------|  Development | Testing |            |
|---------|              |              |---------|------------|
                         |--------------|

In such a system water will flow at a rate of the thinnest pipe. You can't mitigate this by expanding a single pipe, as that will just move the bottle neck elsewhere. Bottlenecks are a disfunction and they'll lead to frutration of the team, and a culture of blaming others for slowing the whole down.

Fixin the problem needs a complete rework of the plumbing, rather thank each team being responsible for their part of the pipe, the team as a whole need to be responsible for the pipe as a whole, this can only happen when the team is equally responsible for the whole:

--------------|--------| 
  Input pipe  |        | 
--------------|  Team  |----------------
              |        |   Output pipe
              |--------|----------------

Note that any team, regardless of scope will have its inputs and outputs, the adoption of CD is fundamentally about teaching teams to group up and share it's respective connections. rather than rebuilding a delivery pipeline overnight, its usual to gradually grow the scope of a teams remit piece by piece. You might start for example by joing the Dev & Architecture functions, and sharing their upstream connection with Product, and downstream with QA. To continue with the metaphor, you replace 2 pipes with one, and do this incrementally until the whoel team is respnsible for its inputs and outputs as a whole. One these 5 are joined there's nothing to stop you widening the principle further!

Business driven deadlines
Team measured in terms of volume of code delivered/hours spent vs value delivered to customers

Tracking the wrong metrics - too much focus on individuals over teams
Technical debt, code quality are things not understood outside of tech team

## developers aren't ready

Monolithic code base - not split into components

More errors in production

Not disciplined enough to check their work before commmitting

No code reviews/pairing

Work 'given' to developers, rather than team self organising

Moving to CD takes enormous amounts of discipline. Nowhere else is this more apparent that with your developers.

## QA aren't ready

There is a general general priciple which states that the cost of fixing a defect increases exponentially the closer to production those bugs are discovered. 

Not many automated tests

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

## external parties aren't ready

external parties on long feedback/change cycles

## customers aren't ready

Customers complain when things change often

don't understand how software is written

don't understand incremental change

not consulted about upcoming changes

no comms channel between tech & customers

## conclusion

