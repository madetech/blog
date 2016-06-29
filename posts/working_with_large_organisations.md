# Cutting through organiations to get stuff done

Over the past year I've worked on a number of projects that have involved some large organisations. By large organisations, I mean, big hefty things that have been around for a while, have lots of cogs and yet still, are achieving lots. 

At Made, our mission is to improve software delivery in every organisation. So working with these lovely organisations is a dream, as there are so many opportunities to help make processes and employees lives so much easier as a result of our engineering and methologies. It gets us excited, and gets us out of bed everyday.

We are a very small company in comparison to these organisations, so we've often felt frustrated when we're unable to deliver software at the speed we like to work. Deploying to production via our continuous delivery piplines happens many times each day, so when things get in the way of that, we call it a smell, and go sniffing out the issues that are clogging things up.

## 1. Get into their offices

At the earliest opportunity, make sure you're able to visit an organisation's office or offices. This is the only real way to see all of the cogs in motion, and hopefully avoids you having to trawl through epic email thread trails where you've no idea who anyone is, or what direction the communication is flowing (see point 8, chat over email).

We were developing a system for a client which sends out completed orders to a warehouse management system, where the staff in the warehouse physically ship goods, and then send status messages back to our systems. It wasn't working. Email wasn't the best way to communicate the issues, and it was a slow process day-to-day waiting for replies.

Being at the clients office for a day turned out to be one of the most productive moves we made for the project. We started with our main contact and then followed the process via people in the UK office, at each stage checking what happened and if there were any issues, until we got to a point where something wasn't right, and then someone was able to resolve it for us to unblock our path to getting our code into a production ready state.

## 2. Shadow staff

When working on feature improvements for a product, request to shadow staff working with the systems day-to-day. See what things are blocking them doing _their_ work, and where real business value can be delivered.

For another client we worked with, by shadowing the staff, we found out that for two days of every work week, the team were having to manually copy and paste orders that had been submitted over the weekend into their sales system. _Two days of copying and pasting._ Instantly, our brains were kicking into action figuring out solutions we'd be able to implement within a few days to help make this process a lot simpler for the staff.

If you're unable to work on improvements there and then, be sure to capture and log improvements that could be made and implemented in the future. We setup a Trello board for things like this.

## 3. Reduce blockers, own the problem

This isn't always feasible and completely depends on the size of your team, and the remit you have with the client. But when working with large organisations, there are often multiple layers to getting simple things done. Often we work in a more agile way to how large organisations have been running for the past decade, so it's not always easy to fit our peg in their hole.

In these cases, we try and take ownership of these things, so that the problem is then our responsibility. An example being infrastructure. When we setup continuous delivery piplines for projects, we often setup multiple servers, and want to be able to create and destroy these as and when needed. Most of the large organisation we've worked with, servers that they use are often snowflakes (read your server is not a pet). They have no automated provisioning, and you can't easily request to have new ones setup, let alone torn down via their IT departments.

When we hit the infrastructure hurdles, we try to set up the resources we require in a separate cloud account, and provide the client with the code that provisions these servers (Terraform/Ansible). The code serves as documentation, and means that we can then reproduce anything we create. If we want to destroy a server, we can create a new one when we need.

## 4. Daily standups

For each project we organise standups that happen at the same time each day. These standups include our team working on the project, as well as key people from the organisation that we're working with. 

It's a great way to show the progress we're making, while at the same time, serves as an opportunity to highlight any blockers to those in the organisation. Sometimes, these can be unblocked easily once raised. Othertimes, not so easy, but if every day you mention the same blocker, it becomes something the organisation can't ignore. It's in these situations people within the organisation are able to put pressure on others to fix it, or the organisation is more willing to accept alternatives they wouldn't normally.

These standups don't have to have the same fixed attendees list throughout a project. For example, if you start working on a different set of features for the project. It's OK to un-invite people from standups! Ensure people present are able to contribute in some manner. 

## 5. Small kanban-esque sprints

With so many cogs in large organisations, it becomes really hard to estimate how long implementing some features will take. If you have to integrate with lots of systems, it becomes near enough pointless to estimate these things. You just don't know what hurdles you'll encounter day-to-day.

Don't estimate all the work. You'll be wasting time on just guessing. Instead focus on smaller sprints that consist of a few days work. Focus on a specific area of functionallity you want to tackle. Setup a Trello board for this sprint. And demo your progress after a day or two to the client, and then at the end of the small sprint.

When starting these sprints, always set a demo date before you begin. The demo must always go ahead, even if you don't get the functionallity in a state you wanted to. In the demo, you can still talk through the progress you've made, and the things that are blocking it from finishing.

Have another Trello board for the more high level epic/roadmap of features. And always be asking the client to assess the priorities of these items. New mini-sprints can then be decided based on this prioritisation. 

As with standups, these small sprint demos allow you to feedback to the client, and in the event thinks couldn't be completed due to blockers, it gives the organisation a chance to re-prioritise based on business decisions. Is this feature worth the time? Or is there something else that would have better business value? A faster feedback cycle is only ever a good thing.

## 6. Isolate legacy systems

We often have to work with existing legacy systems within big companies. It seems that over the years, layers of different solutions are placed on top of one another to fix problems as they're discovered. We're trying to cut away these layers and replace multiple systems with more modern, well engineered, easily extendible replacements.

To do that, figure out the interfaces that these systems interact with. Place logging at each of the entry points to understand what communicates with these systems. Then build a very simple application that can receive these requests and respond in the manner it expects. Then, swap the system out.

If you're able to take control of a few of these layers, eventually you should get to a point where you can then cut out some of the middle layers and merge them into one.

## 7. Chat over email

Imagine having a meeting to decide something that spanned over a week in drips and drabs. Terrifying! That's exactly what important conversations over email turn out to be. Nightmares. Favour chat applications over email. You're able to get answers and make decisions far quicker. If you have a question, ask there and then. Via email, you never know how soon you'll get a response back.

Most chat applications these days have web versions (Slack/Hipchat) that run in the browser, so there is no need to battle those big IT departments that fear any new piece of software will let loose an armada of viruses on their corporate network.

Ensure that you invite everyone who could have valualable insight or knowledge into the chat group. Chat rooms are cheap/free with these tools, so be sure to create multiple ones to try and group conversations together rather than having  a single room with a free-for-all, which will not be productive.

Big businesses often use systems like Lync, so they will probably not be familiar with the Slack/Hipchat style of chatting. Be sure that you explain:

 * How to enable notifications; especially if employees have to run the chat in a web browser
 * Mentions, the @person syntax to direct questions (and notifications) to specific people
 * Where to find different rooms in the group
 * How to attach files
 * How to set themselves as away/do-not-disturb. Sometimes people need to get their head down or attend meetings, don't let this turn into a negative experience for them

Encourage people to have these chat applications open throughout the day.

## 8. Align services before new features

This next point depends on the project you're working on, but for another client, we're rolling out a new ecommerce system across four different European markets. The system we're replacing had different codebases per market, and the goal is to get them all on the same system, so that new features can benefit all markets, while also allowing for a single codebase that is easier to maintain and support.

The approach that has worked really well for us is to get all of the markets onto this new platform, with just the basics of what they currently have to allow them to continue their day-to-day work, and to resist the urge to develop new features. Our new platform is far easier to work with when implementing these things, but getting all markets on the system first means when we come to design new features, we'll consult with all markets so that we engineer a solution that works with them all, either out of the box, via configuration per market, or just disable for markets that don't require it.

Be sure to share with the client (or individual markets) the roadmap. That way they will understand the benefits of holding out in the shorterm while you align everyone, and then the massive positives that will follow when new features start to appear.

***

Working with big organisations doesn't need to be a David vs Goliath battle. The biggest theme from all of the above points is communication. Second is isolating systems and blockers so that you're in control of them. Always push the agile agenda.
