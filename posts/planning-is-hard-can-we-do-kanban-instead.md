# "Planning is Hard can we do Kanban instead"

Planning is an activity that usually results in some emotional response, however it can generally be said that teams avoiding planning will also be avoiding thinking about the future in general. Having a poor engineering strategy can have serious consequences on Lead Time and Delivery Rate.

Whether your experience with planning is a positive or a negative one, it is an skill that must be learnt and mastered.  

When teams start out in Agile they will typically venture towards no planning or Scrum. Implementing Scrum first will generally be an easier task. A good litmus test for when you might be ready to try out more lean/advanced practices is when you feel the need to pivot more frequently than Scrum typically allows you to. 
 
## Ceremonious planning

Traditional (software) project management usually centers around some kind of ceremony when it comes to planning.
This can result in situations where the granularity of planning can be too much, or the decision framework it provides is there to control change to a plan made in a previous planning session.

A good litmus is that when a lot of your planning artefacts are going unused during development, or need to be reworked then it is likely that you are over-planning. You should explore more lightweight alternatives. 
  
This type of environment leads to progressively decreasing productivity. What the business wants to receive is prevented by the same framework that is supposed to aid it. 

Typically ceremonious planning leads to an environment where teams only communicate once per week (or month/quarter), and they are attempting to plan the entire week ahead.

## No planning

An answer to this is to remove planning from the equation! Meeting once a week? Who needs that?

This can work to reduce planning overhead massively, but introduces risk. 

A new problem is introduced: business value adding work is not being prioritised effectively, resulting in business long-term objectives not being met.

One solution is to go back to meeting weekly, right?

## Daily coordination (Scrum)

Scrum answers this with a daily stand up, which has some amount of ceremony attached to it.

- What did you do yesterday?
- What are your plans for today?
- Do you have any impediments?
 
These meetings are to strictly take less than 15 minutes.

This certainly helps teams plan their day within the context of the already planned Sprint(!)

Note well that the Sprint is usually planned every 1-3 weeks, and this can be a fairly heavy-weight session. It is hard for a Scrum team to change course in the middle of a Sprint. Which may feel helpful for teams new to Agile, but highly-performant teams want to be able to change direction on a daily basis!

Scrum requires team members to attend standup at the same time every day, for geographically non-colocated teams, or teams in different time-zones this can be logistically very difficult. This makes Scrum potentially inappropriate for agile teams with these scaling factors.

Moreover it is common for team members new to Agile to be unable to grasp the importance of the daily standup, and to add to the potential pain points it can be time consuming when facilitated badly. 

## Lean-coordination (Kanban)

### What is Kanban?

At the very basic level applying Kanban is as simple as having a Kanban board (e.g. on Trello) to visualise the flow of cards (Kanbans) through a work system.
 
The prevelence of such tools has enabled teams to create Kanban-like flow systems, dubbed ProtoKanban.
  
### What does mature Kanban look like?

#### 1. defined commitment points

It is quite common for Protokanban boards to comprise of To Do, In Progress and Done columns. 
The is a potential sign that there is no defined commitment points, especially if requesters have write access to the board itself.

Risks associated with not having defined commitment points: 

- Perception that your team isn't performant or,
- Perception that Jira/Trello is a black hole for their tasks.
- Knock on effects could be that requesters stop requesting tasks (which can lead to high value items not being ever looked at) or,
- Requesters lose fundamental faith in the ability SD Team (Service Delivery Team)

#### 2. Work in progress limits

To prevent SD Teams committing to **all the work**, Kanban imposes strict WiP limits.

**Work in progress includes work that has been committed to!**

As soon as the SD Team has committed to a work item, the clock is ticking until that work item is considered Done.

This forces teams to meet often with the SRM (Service Request Manager) (roughly to the Product Owner) whenever they have run out of work items to complete.

#### 3. Prioritisation

Kanban coordination generally relies on the SRM pre-prioritising (and pruning) Kanbans before any coordination meetings.
 
Typically the prioritisation approach used by the SRM is centered around urgency modeling, Kanbans with higher urgency make their way to the top of the priority. 

The main purpose of coordination is to apply WSJF (weighted-shortest-job-first), and select the tasks which have the highest Urgency associated with them with the lowest Cost-to-complete.

- Weight is provides by the Urgency model
- Shortest-job is estimated by team members

Highly efficient Kanban SD Teams tackle the shortest-to-deliver most costliest-items-to-delay first.

#### 4. Frequent coordination meetings

This changes the focus of a Kanban coordination from the standard Scrum three questions, to a discussion about the work. 

In other terms - which task am I doing next?

As a result of work in progress limits, Kanban SD Team members will generally meet as-and-when with the SRM. This means the SRM is a role that needs to be highly available.

Due to the heavy work focus of the coordination meetings, Kanban provides less of a feeling of team comradery when compared to Scrum. Adoption of Kanban works best for teams that have already proved that they gel really well. This is partly the cause of another one of the downsides of the Kanban approach: it may fail to discover collaboration issues and/or dependencies.      

As the focus is on delivery to an external stakeholder to the SD Team, Kanban can also hide expectations between SD Team members. Extra effort must be placed on ensuring that internal expectations are voiced. 

## Scaling

It is recommended in Scrum to generally not scale a single team beyond 9-12 members (with even 9 considered extreme by most), by comparison it is generally possible to scale a Kanban flow-system beyond that (with teams seen in the wild at 40-50 members).