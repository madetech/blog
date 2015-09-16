#A Guide to Agile, focused on Scrum.

###Introduction
Over the last few years, we have witnessed the widespread adoption of Agile methodologies across organisations of all shapes and sizes. Some of these organisations have implemented and understood the methodologies well and embrace the Agile manifesto and it's principles. 

However, many people do not really understand and we've witnessed countless organisations who claim to 'be agile', but in reality, they are jumping on the bandwagon and working in ways that could and should not be considered as agile.This concerns me, as I feel like it's going to tarnish the 

At Made, we run all of our software delivery through an Agile methodology called Scrum. We've been using this for the last couple of years and have had some great success with this approach. We're getting to the point where we would consider ourselves experienced practicioners of agile and in this post, we'll provide an introduction to Agile and explain how we use Scrum to deliver projects at Made. 

###What is Agile?
At it's core, Agile is a set of recommendations as to how you approach the delivery of a project. These recommendations are called the 'Agile Manifesto', which is a 15 point list of things that teams should be doing to guide decision making. The recommendations are designed to minimise waste and promote efficiency. For example, favouring communication over documentation and only spending time doing

###The Agile manifesto
###History of Agile
The early versions of Agile were created by Toyoto. They 

###What is Scrum?
Scrum is a project management approach designed to adhere to the recommendations within the Agile Manifesto. 

##Terminology
There is a lot of terminology within Scrum (and Agile) which can be confusing for people not familiar with these practices. I've outlined the 

* ### Spike
A Spike is a fixed period of time used to investigate something which is surrounded in particular uncertainty. For example, you might run a 2 day spike to evaluate the performance of a new technology that hasn't been used before. 

* ### Sprint
A sprint is a timeboxed period (typically between 2-3 weeks) where a team commits to complete a set of completed and shippable user stories. A project is comprised of many sprints.

* ### Velocity
The velocity is the rate at which the team is completing user stories. Once a project is underway and the team is in a rythym, you would expect to see a constant velocity between sprints. Sometimes customers will need to increase this velocity to deliver stories faster and this can be done by increasing team size.

* ### User Story
A User Story is a feature, written from a users perspective. For example, As a Customer, I would like you to remember my credit card details, so I don't have to enter them each time I purchase a product. Use stories are preferential as they allow the team to see the value the business is trying to gain from a feature and this helps it to evaluate different approaches to deliver the value required. 

* ### Story Points
A Story Point is the estimated effort required to complete a User Story. A story point is a relative measure of complexity, rather than a number of hours. My colleague Nick Wood has written about story [points here](blog/story-points) 

* ### Product Backlog
The Product Backlog is the complete list of user stories for a particular project. It should be organised by business value / priority.

* ### Spring Backlog
The Sprint Backlog is the list of User Stories that will be completed in the current sprint. All of the User Stories will have Story Point estimates next to them and the number of Story Points in the backlog should correspond to the velocity achieved over the previous sprints.

* ### Poker Planning
Estimating the complexity of features is particuarly difficult on software projects, so we use Poker Planning to help us to do this. It's a game in which the team are given a set of cards which have the Fibonacachi sequence (1,2,3,5,8,13,21,34,55,89) on them. The Scrum Master describes the User Story and then each team member attending Poker Planning puts a card face down on the table. You all turn over your cards at once and compare and discuss the differences in estimates. We use this technique as it enables us to have fair estimates that the team is agreed upon.

* ### Blockers
A blocker is an impediment which is holding up progress on User Story. For example, if a User Story was to setup Tax Rates for a particular country, but the engineer didn't have the data required to, then this missing data would be considered a Blocker.

* ### Burndown
This is a chart which tracks and visualises the User Stories completed against velocity required to complete a sprint. If for example, the sprint was 10 days long and the team had 100 Story Points to complete, then they would need to complete >10 points per day, to track good progress and have a positive burndownn chart. 

* ### Potentially Shipping Increment
A Potentially Shipping Increment is a piece of functionality which can be launched if the business requires. One of the big focuses in Agile is to limit work in progress and ship frequently, so a big focus is around creating tooling like Continuous Integration, to helps support the deliver of PSIs. 

##Scrum Roles
Within a Scrum project there are a number of critical roles. 

####Product Owner
The Product Owner is in charge of the project vision. It's typically somebody senior within a business, who has the authority to make decisions around direction, features and alignment with the business objectives. Their primary role is to mediate between the internal stakeholders and the Scrum team delivering the project and ensure the team is delivering value to the business in each sprint.

####Scrum Master
The Scrum Master is responsible for day-to-day delivery of the sprint. They lead the ceremonies and work closely with the team to remove any blockers that may be impeding progress. Their job is to protect the delivery team and ensure that work which has been committed to will be complete on sprint showcase.    In a well functioning Scrum team it's healthy to see  a certain amount of tension, between the PO and the SM. Naturally, the PO will want more from the scrum team than is feasible and it's the SM role to ensure the 

####Team
The sprint team is comprised of a number of different people, such as Engineers, Designers, BA's, UX etc. The team will be required to deliver the sprint and typically are full time on the sprint. Sprint teams tend to remain consistent, but can change if the user stories being delivered necessitate the change. 

##Ceremonies
Within Scrum, there are a number of 'Ceremonies' at key moments in the project.The three main ones are: Daily Standup, Sprint Showcase and Retrospective.

####Daily Standup
Every morning at 9am, the sprint team comes together to have their Daily Standup. The 'standup' is a short and informal standing meeting, where the entire team attends and answers three questions: 1) What did you complete yesterday? 2) What are you going to complete today? 3) Is there anything that is blocking you from achieving this?. Standup's are regular opportunity for the entire team to meet and provides an open opportunity for the SM to understand the blockers and cross-polinate information between team members.

At Made (where we work primarily with external customers) we encourage the Product Owner to attend. In stricter Scrum teams, the PO and SM communicate outside of this meeting. 

####Sprint Showcase
On sprint completion a Showcase meeting is organised and run. In the Showcase, all the features which have been completed during the sprint are demo'ed to the Product Owner and any other stakeholders. The idea behind this session is that the team is sharing what should be a shipping increment. Something that the business can release to end consumers and that the business can start seeing some return on their investment from. It's therefore *critical* that at the end of each sprint, the Scrum team are delivering features that are truly launchable. 

####Retrospective
Following Sprint Showcase, a Retrospective is run. This is a fun exercise used to capture feedback from the team on the things that what went well, things that didn't go so well and what learning can be taken into the next sprint. The Agile / Scrum methodologies heavily focus on team improvement and the goal is for the next spint to always be better than the last. This 'always be improving' mentality is really a Agile Manifesto leaning and. The Scrum master organises this session and tends use a game. My colleague Fareed has written about his [Favourite Retrospectives here.](.)

##Meetings
####Backlog Grooming
Once a project is underway, it's easy for the Product Backlog to grow and grow until it becomes a bit of a mess. One of the tasks of the Scrum Master and Product Owner (and sometimes the team) is to sit down together and go through the items in the backlog and remove duplicates and those that are not a priority and are not going to deliver value to the business. 

####Sprint Planning
Before a sprint begins, it's important the team are all aligned and we have up-to-date story points for the features. The role of the sprint planning session is to go through the highest priority items in the backlog and 

##Final thought
XXX
