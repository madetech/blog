#A Guide to Agile, focused on Scrum.

###Introduction
Over the last five years, Agile has gained significant traction and has been adopted by organizations of all shapes and sizes. 

At Made, we have followed suit and now run all of our software delivery through an Agile methodology called Scrum. We've been using this for the last three years and have had some great success with this approach. We're getting to the point where we would consider ourselves experienced practitioners of agile and in this post, we'll provide an introduction to Agile and explain how we use Scrum to deliver software at Made. 

###History of Agile
Agile started to gain traction in early 90's as a reaction to the widespread failure of many large software projects. Back then, the software development process tended to be slow and documentation heavy. The first few months of a project would be spent trying to specify every little detail in a specification document that could easily be several hundred pages long. When required invariably changed, people ended up in dispute and fighting about scope change and cost adjustments. Obviously people realised there were better and more efficient ways and Agile was introduction.  

###What is Agile?
At its core, Agile is a set of principles that are be used to guide the delivery of a software project. Agile encourage an iterative approach to software delivery that is built incrementally from the start, instead of trying to deliver it all in one lump at the end.

It works by breaking projects down into small chunks of functionality called user stories, prioritizing them, and then delivering them in short cycles called iterations.

###The Agile Manifesto
Agile has some key concepts. Firstly there is the Agile Manifesto which is 5 points that define what an Agile team should value:

1. Individuals and interactions over processes and tools
2. Working software over comprehensive documentation
3. Customer collaboration over contract negotiation
4. Responding to change over following a plan

In addition to these, Agile practitioners also have a more granular list of principles:

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

###What is Scrum?
Scrum is an Agile methodology. It follows the principles set out in the Manifesto but has some additional concepts that are specific to it, such as Sprints, Product Owner, etc. The name Scrum comes from the sport of Ruby, as the team needs to work together to deliver a common goal.   

###How does Scrum work?
[![alt text](https://www.mountaingoatsoftware.com/system/asset/file/17/ScrumLargeLabelled.png "Scrum Diagram")](https://www.mountaingoatsoftware.com/system/asset/file/17/ScrumLargeLabelled.png)

##Terminology
There is a lot of terminology within Scrum (and Agile) which can be confusing for people not familiar with these practices. I've outlined the key concepts below:

* ### User Story
A User Story is a feature written from a user's perspective. For example, "As a Customer, I would like you to remember my credit card details, so I don't have to enter them each time I purchase a product". User stories are preferred to feature lists as they allow the team to more easily understand the value to the business. 

* ### Product Backlog
The Product Backlog is the complete list of user stories for a particular project. It should be prioritized by business value.

* ### Story Points
A Story Point is the estimated effort required to complete a User Story. A story point is a relative measure of complexity, rather than some number of hours. My colleague Nick Wood has written about story [points here](blog/story-points) 

* ### Spring Backlog
The Sprint Backlog is the list of User Stories that will complete in the current sprint. All of the User Stories will have Story Point estimates next to them, and this total should align with velocity achieved in the previous sprints.

* ### Spike
A Spike is a fixed period used to investigate something that has particular uncertainty. For example, you might run a 2-day spike to evaluate a new technology that the team hasn't used before. 

* ### Sprint
A sprint is a timeboxed period (typically between 2-3 weeks) where a team commits to complete a set of defined User Stories. A project is comprised of multiple sprints.

* ### Velocity
Velocity is the rate at which the team is completing user stories. Once a project is underway, and the team is in a rhythm, you would expect to see a consistent velocity across sprints. Occasionally customers need to deliver features quicker. This can be achieved by increasing the team size and therefore the velocity.

* ### Poker Planning
Estimating complexity is particularly difficult in software projects. We use Poker Planning to help us to do this. It's a card game in which the team is given a set of cards that have the Fibonacci sequence on them. The Scrum Master describes the User Story and each team member puts a card face down on the table. All cards are then turned over at once, and then the team discusses the differences in estimates. This technique enables us to have fair estimates that the team has agreed.

* ### Blockers
A blocker is an impediment that is holding up progress on User Story. For example, if a User Story was to setup Tax Rates for a particular country, but the engineer didn't have this data. The missing data would be considered a Blocker. Blockers should be flagged to the Scrum Master.

* ### Burndown
The Burndown chart tracks and visualizes the User Stories completed against velocity required to complete a sprint. If a sprint was ten days long, and the team had 100 Story Points to complete, then the team would need to complete 10+ points per day, to track good progress and see a positive burndown chart. 

* ### Potentially Shipping Increment
A Potentially Shipping Increment is a piece of functionality which can launch on completion. One of the big focuses in Agile is to limit work in progress and ship frequently. There is lots of tooling like Continuous Integration Environments, which help to support the delivery of PSIs. 

* ### Backlog Grooming
Once a project is underway, it's easy for the Product Backlog to grow and grow until it becomes a bit of a mess. One of the tasks of the Scrum Master and Product Owner (and sometimes the team) is to sit down together and go through the items in the backlog and remove duplicates and those that are not a priority and are not going to deliver value to the business. 

* ### Sprint Planning
Before a sprint begins, it's important the team are all aligned, and we have up-to-date story points for the features. The role of the sprint planning session is to go through the highest priority items in the project backlog and agree. 

##Scrum Roles
Within a Scrum project there are some key roles that are necessary:

* ####Product Owner
The Product Owner is in charge of the project vision. This person is typically somebody senior within a business, who has the authority to make decisions about direction, features and alignment against the business objectives. <br /><br />Their primary role is to mediate between the internal stakeholders and the Scrum team delivering the project and ensure the team is delivering the most value to the business in each sprint.

* ####Scrum Master
The Scrum Master handles day-to-day delivery of the sprint. They lead the ceremonies and work closely with the team to remove any blockers that may be impeding progress. <br /><br />The Scum Master's job is to protect the delivery team and ensure that committed work will be complete for Sprint Showcase. In a well-functioning Scrum team, it's healthy to see a certain amount of tension, between the PO and the SM. Naturally, the PO will want more from the scrum team than is feasible and it's the SM role to help the team delivers consistently and not be overworked by the PO.

* ####Team
A sprint team consists of some different people, such as Engineers, Designers, BA's, UX, etc. The team will be required to deliver the sprint and typically are full-time on the Sprint. Sprint teams tend to remain consistent but can change if the user stories being delivered necessitate the change. 

##Ceremonies
Within Scrum, there are ceremonies at key moments in the project. The three main ones: Daily Standup, Sprint Showcase, and Retrospective.

* ####Daily Standup
Every morning at 9am, the sprint team comes together to have their Daily Standup. The 'standup' is a short and informal standing meeting, where the entire team attends and answers three questions: 1) What did you complete yesterday? 2) What are you going to complete today? 3) Is there anything that is blocking you from achieving this?. Standup's are regular opportunity for the entire team to meet and provides an open opportunity for the SM to understand the blockers and cross-pollinate information between team members.<br /><br />At Made (where we work primarily with external customers) we encourage the Product Owner to attend. In stricter Scrum teams, the PO and SM communicate outside of this meeting. 

* ####Sprint Showcase
On sprint completion, a Sprint Showcase meeting takes place. In the Showcase, all the completed features are showcased to the Product Owner and any other stakeholders. The idea behind this session is that the team is sharing what should be a shipping increment. Something that the business can release to end consumers and that the business can start seeing some return on their investment from. It's, therefore, *critical* that at the end of each sprint, the Scrum team are delivering features that are truly launchable. 

* ####Retrospective
Following Sprint Showcase, a Retrospective is run. This is a fun exercise used to capture feedback from the team on the things that what went well, things that didn't go so well and what learning can be taken into the next sprint. The Agile / Scrum methodologies heavily focus on team improvement and the goal is for the next sprint to be better than the last. This 'always be improving' mentality is key to Agile. My colleague Fareed has written about his [Favourite Retrospectives here.](.)