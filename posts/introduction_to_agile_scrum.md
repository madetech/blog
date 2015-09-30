#Introduction to Agile and Scrum

###Preface
Over the past five years, Agile has gained significant traction and has been adopted by organizations of all shapes and sizes. 

At Made, we run all of our software delivery through an Agile methodology called Scrum. We've been using Scrum for the last 3 years and have had some great success with it. 

We're getting to the point where we would consider ourselves experienced practitioners of agile, so in this post, we'll share some of our learnings and provide an introduction to Agile and explain how we are using Scrum to deliver software at Made. 

###History of Agile
Agile started to gain traction in early 90's as a reaction to the widespread failure of many large software projects. Back then, the software development process tended to be slow and documentation heavy. The first few months of a project would be spent detailing everything within a specification document that was often several hundred pages in length. Nobody ever read these documents, but when requirements invariably changed, people ended up in dispute and claims of scope and cost adjustments ensueed. People realised there must be a better and baby Agile was born.

###What is Agile?
At its core, Agile is a set of principles that can be used to guide the delivery of a software project. It encourages ongoing collaboration and advocates software being delivery incrementally from the start, instead of trying to deliver it all in one lump at the end. 

###The Agile Manifesto
The bible has the ten commandments. Ghandi has the XX. Agile practicioners follow The Agile Manifesto: 

1. **Individuals and interactions** over processes and tools
2. **Working software** over comprehensive documentation
3. **Customer collaboration** over contract negotiation
4. **Responding to change** over following a plan

The Manifesto is embraced by all good Agile teams and although they will value the right hand side (the text that is not in bold), they will always look to favour the left hand side (text in bold). You'll often hear Agilists citing items from the Manifesto as a rationale behind a decision or approach. 

In addition to the manifesto, Agile practitioners also follow a more granular set of principles, which guide the day-to-day running of a an agile project:

1. The highest priority is to satisfy the customer through the early and continuous delivery of valuable software.
2. Welcome changing requirements, even late in development. Agile processes harness change for the customer's competitive advantage.
3. Deliver working software frequently, from a couple of weeks to a couple of months, with a preference to the shorter timescale.
4. Business people and developers must work together daily throughout the project.
5. Build projects around motivated individuals. Give them the environment and support they need, and trust them to get the job done.
6. The most efficient and effective method of conveying information to and within a development team is face-to-face conversation.
7. Working software is the primary measure of progress.
8. Agile processes promote sustainable development. The sponsors, developers, and users should be able to maintain a constant pace indefinitely.
9. Continuous attention to technical excellence and good design enhances agility.
10. Simplicity--the art of maximizing the amount of work not done--is essential.
11. The best architectures, requirements, and designs emerge from self-organizing teams.
12. At regular intervals, the team reflects on how to become more effective, then tunes and adjusts its behavior accordingly.

#Scrum
Scrum is an Agile methodology. Its name comes from the sport of Rugby, where a team needs to work together to drive forward and achieve a common goal. It follows the principles set out in the Agile Manifesto, with some additional concepts that sit on-top of it, such as Sprints, Product Backlog, Daily Standup etc.<br /><br />Scrum is the most popular of the Agile methodologies, so it can be seen as the same thing as Agile. **It's not**, and you should explain the difference when you hear people refer to Agile and Scrum as one.

###How does Scrum work?
[![alt text](https://www.mountaingoatsoftware.com/system/asset/file/17/ScrumLargeLabelled.png "Scrum Diagram")](https://www.mountaingoatsoftware.com/system/asset/file/17/ScrumLargeLabelled.png)

##Terminology
There is **a lot** of domain specific terminology within Scrum, which can make it difficult to understand and adopt as a newbie. For those who are not familiar with its practices, I've outlined the key concepts below:

* ### User Story
A User Story is a feature written from a user's perspective. For example, "As a Customer, I would like you to remember my credit card details, so I don't have to enter them each time I purchase a product". User stories are preferred to feature lists as they allow the team to more easily understand the business value. 

* ### Product Backlog
The Product Backlog is a list of user stories for a particular project. It is prioritized by business value.

* ### Story Points
The Story Point is the estimated effort required to complete a User Story. A story point is a relative measure of complexity, rather than some number of hours. We have written a more detailed article which [explains story points here](blog/story-points).

* ### Spring Backlog
A Sprint Backlog is a list of User Stories that the team should complete during a sprint. All of the User Stories will have Story Point estimates next to them, and this total should align with velocity achieved in the previous sprints.

* ### Spike
A Spike is a fixed period used to investigate uncertainty. For example, you could run a 2-day spike to evaluate a new technology that the team hasn't used before. 

* ### Sprint
A sprint is a timeboxed period (typically between 1-4 weeks) where a team commits to complete a set of defined User Stories. A project is comprised of multiple sprints.

* ### Velocity
Velocity is the rate at which the team is completing user stories. Once a project is underway, and the team is in a rhythm, you would expect to see a consistent velocity between sprints. 

* ### Planning Poker
Estimating complexity is particularly difficult in software projects. Scrum uses Planning Poker to help with this. It's a card game in which the team is given a set of cards that contain a modified Fibonacci sequence on them: 1, 2, 3, 5, 8, 13, 20, 40 & 100. The numbers get further apart as you get higher to emphasise bigger things are inherently harder to estimate.<br /><br />The Product Owner describes the User Story and each team member puts a card face down on the table. All cards are turned over simultaniously, and then the team discusses the differences in estimations. This technique encourages discussion and helps to provide fair estimates that the team is agreed upon.

* ### Blockers
A blocker is an impediment that is holding up progress on User Story. For example, if a User Story was to setup Tax Rates for a particular country, but the engineer didn't have this data. The missing data would be considered a Blocker. Blockers should be flagged to the team and if the team cannot resolve them, then the Scrum Master should try to.

* ### Burndown
The Burndown chart visualizes the progress against velocity and provides an early warning system if the team are tracking behind the intended target. If a sprint was ten days long, and the team had 100 Story Points to complete, then the team would need to average upwards of 10 points per day, to track good progress and see a positive burndown chart. 

* ### Potentially Shipping Increment
A Potentially Shipping Increment is a piece of functionality which can launch on completion. One of the big focuses in Agile is to limit work in progress and ship frequently. There is lots of tooling like Continuous Integration Environments, which help to support the delivery of PSIs. 

* ### Backlog Grooming
Once a project is underway, it's easy for the Product Backlog to grow and grow until it becomes a bit of a mess. One of the tasks of the Scrum Master and Product Owner (and sometimes the team) is to sit down together and go through the items in the backlog and remove duplicates and those that are not a priority and are not going to deliver value to the business. 

* ### Sprint Planning
Before a sprint begins, it's important the team are all aligned, and we have up-to-date story points for the features. The role of the sprint planning session is to go through the highest priority items in the project backlog and agree. 

##Scrum Roles
Within a Scrum project there are a number of key roles that are necessary:

* ####Product Owner
The Product Owner is in charge of the project vision. This person is typically somebody senior within a business, who has the authority to make decisions about direction, features and understands the business objectives. <br /><br />Their primary role is to mediate between the internal stakeholders and the Scrum team delivering the project and ensure the team is delivering the most value to the business within each sprint.

* ####Scrum Master
The Scrum Master handles day-to-day delivery of the sprint. They lead the ceremonies and work closely with the team to remove any blockers that may be impeding progress. <br /><br />The Scum Master's job is to protect the delivery team and ensure that committed work will be complete for Sprint Showcase. In a well-functioning Scrum team, it's healthy to see a certain amount of tension, between the PO and the SM. Naturally, the PO will want more from the scrum team than is feasible and it's the SM role to help the team delivers consistently and function well.

* ####Team
A sprint team consists of some different people, such as Software Engineers, Designers, Business Analysts, User Experience, etc. The team will be required to deliver the sprint and typically work full-time on the Sprint. Sprint teams tend to remain consistent but can change if the user stories being delivered necessitate the change. 

##Ceremonies
Within Scrum, there are ceremonies at key moments in the project. The three main ones being: Daily Standup, Sprint Showcase, and Retrospective.

* ####Daily Standup
Each morning, the sprint team comes together to have their Daily Standup. The 'standup' is a short and informal standing meeting, where the entire team attends. Each team member answers the following three questions:<br />
1. What did you complete yesterday?
2. What are you going to complete today?
3. Is there anything that is blocking you from achieving this?.
<br />Standups are regular opportunity for the entire team to communicate progress, understand blockers, cross-pollinate information and evaluate risks.<br /><br />At Made (where we work primarily with external customers) we encourage the Product Owner to attend. 

* ####Sprint Showcase
On sprint completion, a Sprint Showcase meeting takes place. In the Showcase, all the completed User Stories are showcased to the project stakeholders. The idea behind this session is that the team is sharing what should be a shipping increment. Something that the business can release to end consumers and that the business can start seeing some return on their investment from. It's, therefore, *critical* that at the end of each sprint, the Scrum team are delivering features that are truly launchable. 

* ####Retrospective
Following Sprint Showcase, a Retrospective is run. This is a fun exercise used to capture feedback from the team on the things that what went well, things that didn't go so well and what learning can be taken into the next sprint. The Agile / Scrum methodologies heavily focus on team improvement and the goal is for the next sprint to be better than the last. This 'always be improving' mentality is key to Agile. My colleague Fareed has written about his [Favourite Retrospectives here.](.)


##Putting this into practice
So, how does all of this work within Made?<br /><br />
1) **Before the project **We'll typically kickoff a project by running a story planning workshop. (You can see the presentation we use for this here.)[Link to Nick's deck]. In this workshop we'll capture an initial product backlog and work with the attendees to prioritise stories into an appropriate order. We'll take the backlog back to the team and run an initial high level pa
2) **Before the first sprint** - We'll run a Planning Poker session with the entire team. We'll add Story Point estimations to the highest priority items in the Product Backlog and create a sprint candidate for review by the Product Owner
3) **Kickoff sprint** - We'll then move into the sprint. Each

##Where next?
In more recent years, Agile principles have started to be adopted by non-software projects and you see XX