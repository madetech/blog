# Let your teams plan for themselves

As an industry of tinkerers, optimisers and perfectionists we occasionally miss the beauty of unorganisation and human instinct. Our obsession to be more efficient and productive can sometimes have some undesired consequences. At Made we often adapt our processes in the name of efficiency but lately we've started experimenting by taking away some of these processes with surprising results.

In a recent [Clojure Gazette][clojure-gazette], Eric (hello Eric!) wrote about management trying to *protect* the time of engineers so they can do their job of *programming* without distractions:

> You start to protect their time. You think "I'll make all of these decisions for them. I'll write them up and divide them into little pieces and prioritize them. All they'll have to do is pull one down and start working on it. I can even ask the designers myself for some work. I won't bother the programmers with it until the designers are finished."

I can relate to this as it can often be tempting to setup a Trello board, calculate (guesstimate) a deadline and hand it to a team. Programmers want to program right? I've sat through hours of backlog grooming sessions and sprint planning meetings so I know how often they can feel both boring and useless. So why not keep the majority of the team out of planning?

The issue with keeping your team shielded from planning is that they lose the context in which they are trying to solve problems. By spoon feeding a team you are taking responsibility from them, you are removing their ownership of the problem. This can be a big demotivating factor, after setting out to increase efficiency you can end up with a disinterested team coding features to a specification and fixing a list of bugs with no context.

We decided recently to take a different approach, instead of removing developers from planning we decided to leave planning up to developers. We hoped this would allow teams to take more ownership of delivery. By having a higher level of understanding behind the problem we thought teams would be able to solve them better. We recognise that an increase in responsibility usually correlates to an increase in happiness and therefore performance.

Instead of maintaining a backlog of stories along with grooming sessions and sprint planning meetings we tried an alternative agile approach. We moved to maintaining a high level roadmap of problems or goals. Once a team became available we would pull of the highest priority goal off the roadmap and handed it over to the team for an iteration.

1. **Briefing**
   The team is introduced to stakeholders of the goal and then given a walkthrough of the problem domain for around 15 minutes.
2. **Discovery**
   The team then goes away to think about how they might solve the problem. Sometimes this might require a day or two of spiking.
3. **Planning**
   The team then plans in whatever way they prefer. Most favour a simple Trello board with columns for "Must", "Should", "Could", "Doing" and then "Done". The team would announce a date for initial and final showcases to stakeholders along with the scope they are expecting to tackle.
4. **Development**
   The team begins development on the problem. This is the "programming" bit most of the time.
5. **Showcase**
   The team will first give an initial showcase within a day or two of starting development. This allows them to collect feedback from stakeholders based on assumptions they've been making. The team then repeats steps 4. and 5. every couple of days until the final showcase. The final showcase will demo a production deployed solution.
6. **Monitoring**
   The team will typically monitor any deployments for the next few days whilst starting their next iteration. Sometimes a day or two will be dedicated to monitoring if we expect a bunch of tasks to fall out though this sometimes will itself turn into a subsequent iteration.

With this workflow, our full stack engineers own each iteration and determine how it is run all the way to production.

In a Signal versus Noise article [on Permission][permission], Jason Fried talks about the benefits of handing over responsibility:

> When the person doing the work is the person that has to live with the consequences, they tend to think more completely about what they’re about to do. They see it from more angles, they consider it differently, they’re more thoughtful about it because it’s ultimately on them.

We really agree with this sentiment and have found every time we hand more responsibility to teams the better the results.

We're advocates for small teams of full stack developers rather than building larger teams with specialised roles. We typically do not have non-technical roles within teams. We want our engineers to act as project managers, agile coaches, customer liason, testers and more. We want a team to be able to fully engage with a problem from start to finish and find full immersion into a problem provides this.

We've been using this workflow on a number of engagements for over 6 months now and have not missed traditional scrum one bit! Scrum originally had the benefit of allowing us to provide estimates for when features could be delivered. Even though we now work with high level roadmap items that aren't estimated, we still work to a timeline. Clients have an idea of a deadline for goals and teams will have to negotiate the scope of their iteration.

In planning, teams will grade work into "Must", "Should" or "Could" by having conversations with stakeholders. If a client requires something by a certain date the team will accommodate this by limiting scope further, perhaps into shorter iterations so we can have finer grained control over what is delivered. If an iteration ends with unfinished tasks, we often find they are in the "Could" column and end up being dropped altogether.

In larger organisations our practices would likely be met with adversity and this sometimes does happen with our customers. We often try out practices such as [#noestimates][noestimates] and #noplanning in a small trial project with the aim to using them more widely. In reality we often find a balance between how we'd prefer to work and what our customers are comfortable with whilst still pushing new ideas where we can.

In letting go of more traditional management of team workloads and planning of delivery we have found deadlines are still met and teams appear happier to be in more control of their work. We've even implemented this strategy in our customer's engineering teams to much success.

Has your team recently tried reducing the bureaucracy around teams and delivery? Perhaps your team wants to try some aspects of #noestimates and #noplanning? Get in touch with us on Twitter @madetech_com!

[clojure-gazette]: http://www.clojuregazette.com/
[permission]: https://m.signalvnoise.com/if-you-ask-for-my-permission-you-wont-have-my-permission-9d8bb4f9c940#.mpx625wqy
[noestimates]: https://www.madetech.com/blog/7-reasons-to-adopt-number-noestimates-in-software-delivery
