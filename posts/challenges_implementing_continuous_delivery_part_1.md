# Organisational challenges with adopting Continuous Delivery #

Adopting continuous delivery for a single team is tough, adopting it across a whole organisation is exponentially more. It's hard to catalogue all the issues a business may face during a transition, but I wanted to catalogue the common pitfalls. In the first of two posts I will discuss the organisational challenges, and in part II, Chris will discuss the technical challenges.

# Giving Teams Ownership

In a 'traditional' software setup, with separate teams (commonly: product, architecture, development, QA, Ops, plus a few others) a move to continuous likely impossible unless you have exceptional levels of communication between all teams. When each team is only responsible for their own output, without strong discipline it's hard to stave off a culture of 'throwing things over the wall' to the next team in line.

You feature pipeline might look something like this - it's ominously Waterfall:

[Product Team] => [Architecture] => [Software devlopment] => [QA] => [Ops]

On close inspection its apparent that this pipeline isn't very fault tolerent. A failure in any single team prevents anyone else from doing their job! The other challenge  is how to ensure that each of the five teams are working at the exact same rate. If the Product Team are defining features faster than they can be architected, then we have a bottleneck. Items are sitting idle in the architecture queue, waiting for someone to pick them up. Over time this leads to a massive Architecture backlog which becomes impossible to prioritise, and business goals may have changed by the time architecture get around to tackling them.

The opposite problem is equally likely, and is probably happening simultaneously elsewhere in your process. Lets imagine the development team can build features faster than the architects can specifiy them, and also faster than QA can test them. Well now there's a very real chance that your developers will run out of stuff to do, those bums on seats are costing you money and you're getting no return on that investment.

NB. I don't mean to say that architecture is the problem, they are just an example - your botteneck could be anywhere.

In the example described above your pipeline looks like this. With the width of the pipe in some sense indicating the rate of work:

|---------|--------------|--------------|         |------------|
> Product > Architecture >              |---------| Deployment |
|         |--------------|  Development > Testing >            >
|---------|              |              |---------|------------|
                         |--------------|

In such a system the flow of the whole is ultimately determined by the flow of the slowest team. Any team capacity above this is essentially wasted. As a stop gap you could expand your slower team to improve throughput, but ultimately all you will do is move the bottleneck elsewhere. Bottlenecks are a disfunction and they'll lead to frutration of the team, and a culture of blaming others when they inevitable slow the system down.

Fixing the problem needs a complete rework of the plumbing. Rather than each team being responsible for their part of the pipe, the team as a whole need to be responsible for the entire throughput of the system, this can only happen when the team is equally responsible for the whole:

|--------------|-----------------------| 
>  Input pipe  >                       | 
|--------------|  Team Responsibility  |---------------|
               |                       >  Output pipe  >
               |-----------------------|---------------|


Any team, regardless of scope will have its inputs and outputs, the adoption of CD is fundamentally about teaching teams to group up and share their dependencies, rather than being co-dependent on each other. Such a transformation won;t happen overnight though. Adopting this change in thinking can usually be accomplished in several discrete steps. You might start for example by joing the Dev & Test functions, by having testers and developers work closely with Architecture to define technical requirements. Testers can then write their tests whilst the developer writes their code, and as they are both working on the same thing it's much easier for them to talk through issues to reach a common understanding.

The team should also share ownership of their output stream too , ensureing that nothing goes to the Ops team until developers and testers alike are both happy. No more arguments along the lines of "Testing should have caught the bug" - the team either succeed together, or fail together.

Ensuring everyone is utilised effectively will likely require some element of cross skilling, ensuring your devs know how to test code, and testers understand the system architecture are all valuble side effects of the transition. That's not to say that there's no room for specialisation though - our  goal isn't to have everyone equally skilled in all areas, just to ensure that everyone understands and is responsible for how the whole team works.

# Measuring Success

A key difficulty with Continuous delivery, is changing how to measure success/progress. Many Agile methodologies start to fall down when faced with genuine continuous delivery. Take Scrum as one example, what value does a Sprint Demo have in such an environment? In a two week sprint we'll have close to a dozen features in production by the end so is there value sitting stakeholders down and running through features they've likely already seen? How does measuring a teams velocity over two weeks help us figure out where bottlenecks are so that we can improve? It's likely in such an environment that average cycle time - i.e. how long it takes to go from inception to production - will be a much more meaningful metric.

Delivering value to customers is the ultimate goal of any software project, actually measuring this is generally quite difficult with a large change set though. Once you are delivering atomic units of value in a continuous delivery fashion it becomes much easier to measure this. By tracking key performance metrics from build to build you can easily see which builds had the biggest impact on value (conversion rate, or average session time being two common examples). Combine this with cycle time and you have two very powerful tools for determining the most valuable work for the team to focus on next.

# Setting Deadlines

Broadly speaking, there are two kinds of deadlines - I called them hard and soft deadlines. I define them as follows:
* Hard deadlines - a fixed date in the calendar, where something must be delivered otherwise significant business harm will result. i.e. We'll go bust or suffer severe reputaional damage if this isn't done by a certain date.
* Soft deadlines - everything else. 

Most deadlines are soft deadlines, but a common disfunction is for soft deadlines to be treated as hard ones. 

How your business treats deadlines is a useful indicator of how successfully they might adopt continuous delivery. The following are all 'smells' which are going to make CD difficult:
 * Soft deadlines frequently masquerading as hard deadlines - "We promised customer X this feature by March" is a soft deadline, not a hard one.
 * Teams have no control over their soft deadlines - customers are promised feature by a given date with no involvement of the team
 * Teams are punished for failing to meet soft deadlines

In an ideal world there are no hard deadlines, and the team are able to set their own deadlines. Reaching this ideal is a tough slog though, and requires lengthy periods of building trust between engineers and business people. Developers need to trust the business to communicate estimates, **as estimates**, to stakeholders, and not use them as tool to make teams to work extra hours. Similarly salespeople need to trust developers to set realistic expectations of what they can deliver, and also to meet the majority of the deadlines they set.

# Managing Technical Debt

It's relatively uncommon for the concepts of technical debt & code health/quality to be well understood outside of your immediate tech team. Which is a shame, as these have a massive impact on your teams ability to perform - or as we defined it above, cycle time. Exposing these metrics as loudly as you can is a great way to encourage the business to take more of an interest in them, and to prioritise improving them. It's much easier to make the business care about these metrics when faced with concrete data; such as "We spent a week on increasing test coverage in this section of our application by 50%, and sped up build times by 15% - this has removed a day from our mean cycle time for this component meaning we can get new features in front of customers 10-20% faster." The converse is also true "Test coverage has dropped this month 20% and as a result we've seen more build failures and an increased cycle time" is a great way to make financially incentivised people care about you code health, and give teams space to take rededial action.

That's not to say our aim is to remove technical debt completely - consider treating technical debt like a financial one. Having lots of debt is probably a bad thing, but if you have a good rate of interest, debt becomes managable, and in some cases even desired (lots of companies run at a defecit, and most homeowners have a mortgage for example). Paying off the entire debt in one go is probably not practical - but in order to get the debt under of control it's important to keep up with interest (i.e make sure you are not making your technical debt worse) and make regular down payments (take active steps towards improving the state of your codebase). Technical debt is hard to measure, but using the metaphor above it can be understood by imagining our 'interest' as a tax on every release. The more releases we do, the more important it is to keep this under control.

## Helping Customers Embrace Change

Arguably the hardest relationship to maintain as a software company is the one with your most important resource - your customers. They can also be one of the biggest challenges to continuous delivery. Changing your application frequently has both the ability to empower or frustrate your entire user base. As with many things, the devil is in the details.

Unless you're working in the rarified sector of delivering software to other developers, then it's highly likely that you customers don't understand how software is made at anything more than a superficial level. The first quesiont you must ask youself when adopting CD is 'can our users handle a constantly evolving product?'. If the answer to this question is 'no' then it's possible that continuous delivery is not for you.

An alternative approach might be to split your product into different 'release streams' i.e. a stable branch for customers who don't want change, and a alpha/beta channel for those who embrace it. This in some sense gives you the best of both worlds - as you can readily get feedback from your alpha channel customers. They feel more loved as they feel like they are being listened too - and have a very real impact on shaping the product which they use.

Mutliple release channels does add an overhead to every release, however, so this approach should be used with caution. It also probably wouldn't strictly be defined as Continuous Delivery, but if it's your only barrier to CD then you might consider it worthwhile.

## To Sum Up

Continuous Delivery has a mutlitude of downsides if done poorly, but it also has tremondous potential upside if done well. If you're planning on adopting some CD principles I hope this article has helped you see ahead to where your organisation might run into problems. Next Time Chris is going to talk through the technical challenges associated with Continuous Delivery.