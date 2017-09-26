# Where to start with cloud migration?

Your organisation has decided it's ready to move to the cloud. Where do you start?

Defining a roadmap isn't as simple as writing a list of servers that need migrating. Cloud migrations are very rarely a one to one lift and shift from on-premise to a cloud provider like Amazon Web Services.

Not only are migrations not as simple as lift and shift, the prioritisation of what to move and when is fundamental to making a migration successful. Knowing how to phase the migration into many small steps is crucial for reducing risk.

There are a number of questions that can help inform your roadmapping process.

## What are your mission critical applications?

Changes to mission critical applications will have significant risks associated, 
will likely impact other applications, and will potentially be the most disruptive to the organisation. It is for these reasons that mission critical applications should be tackled first.

If your business sells products and services to customers via an application then this system will likely be mission critical. Systems such as a trading platforms or bespoke software, perhaps even running in your customers premises, are also likely to be critical.

If your business uses software in order to function, and let's face it, this is most organisations, which systems could cause serious damage to your business if they disappeared for a few hours, minutes, or perhaps even seconds?

Breaking this analysis down into processes or workflows can also be useful. A single application may well provide multiple processes and workflows of which only a subset are mission critical. It's important to split these out.

Now you have a list of mission critical functionality, you have the beginnings of your roadmap.

## What are the goals behind your migration?

Modernisation and cost savings are great supporting arguments for moving to the cloud but they aren't the only goals that should be driving your migration.

In order to decide how to break the migration into reasonable chunks, and in order to be able to prioritise what to move first, goals that focus on improving the business value provided by existing applications is essential. I'll illustrate what I mean with a couple of examples.

### Example one: Large monolithic business application

Our first example is that of an application that is a business's central database, provides workflows for business processes, is the CRM, and provides accounting tools for an organisation that is currently running on-premise. Clearly the organisation is tied into the application and as such a migration to the cloud could prove quite disruptive.

Lift and shift would be difficult because such systems often rely on running on the users machine, having access to local printers, accessing a database on the local network, shared storage, and likely more ties that make it hard to remove from on-premises. Not only this but it would also require switching the entire business over to the new system all at once seeing as everything is tied into a single system.

A byproduct of understanding how locked in the business is to the single application, and understanding how risky an all-in-one migration might be, there may be significant business value to be gained from breaking down the monolith into smaller focussed applications. Breaking an application down into applications per process or workflow would mean the migration could happen process by process or department by department. This would be less risky than moving the whole business at once.

Moving accounting and CRM to off-the-shelf SaaS products would mean two less pieces to move across and also mean you could benefit from using software that focusses on doing one thing and one thing well.

From this analysis, 2 additional goals for the migration could be defined:

- Decouple business software and processes from one another in order to enable easier change in future
- Move to off the shelf software where possible so engineering efforts can be spent in more relevant areas (rather than reinventing the wheel for accounting and CRM)

### Example two: Focussed supply chain application

In our second example, a business has a set of more focussed applications. One of their mission critical systems is their supply chain tool that manages stock ordering. The application is by all accounts ripe for the picking, however there have been many complaints from the business that due to the poor user experience of the application, it is a source for a lot of bad data within the business. Inconsistent product naming, many records in the product database for the same product with only subtle differences are among many data quality issues.

Migrating the application as it currently is won't be providing any new business value and also will be extending the life of software that is currently a poor fit for the business. It might be wise to use this opportunity to improve the user experience of the software, running the new version in the cloud alongside the existing version means an easier transition for the business, and an opportunity to improve data quality before switching off the legacy system.

From this analysis we can define a new goal for the migration:

- Improve quality of data being entered into system

Both of these examples are real strategies we've applied to two separate customers successfully. Cloud migration must be tied to significant business value, otherwise the migration may perpetuate legacy problems.

By defining business goals that provide new value you can make decisions on how to approach the migration.

## How cloud ready are your applications?

Understanding how cloud ready your applications are is important as it will likely impact how you approach the migration.

What kind of system dependencies do your applications have? Are they operating system dependant? For example, do they have to be run on Windows? Do they require other software to be installed on the systems on which they run? Answers to these questions can change how a migration might be approached.

How is your application consumed? Do users access it via a web browser? Is it accessed via an intranet or VPN? Is it connected to via a remote login session? Again, answers to these questions will affect the roadmap.

If your application backs onto a database or other service like SMTP for sending emails then these two will need to be migrated. If you can change where you application looks for these services via configuration, you're lucky. A lot of legacy applications will have hard dependencies that are not so easy to change.

You may recognise some of these questions if you are familiar with ["The 12 Factor App"](https://12factor.net/). This seminal document defines 12 properties of a cloud ready application.

If you plan to create new applications, especially if you're breaking a large legacy system into smaller pieces, then this is a great time to ensure your applications are cloud ready.

## How ready is your organisation for a cloud migration?

Change in an organisation is always a challenge. The larger the organisation the harder change becomes. Migrations are both disruptive and technically demanding.

By breaking down migrations into smaller steps, disruption will be mitigated somewhat, attention to timing with other milestones in the organisation is important. Changing e-commerce systems just before Black Friday and Christmas period is a risky approach. Replacing accounting software at year end is also likely to be more disruptive than necessary.

Organisations that have traditionally used on-premise servers or datacenters for running their systems may be lacking skills required for a cloud migration. The toolsets for cloud can differ from more traditional approaches. The use of automation tools like Ansible, Capistrano and Fabric may be less familiar. Using such tools to create and scale servers will certainly be unfamiliar. Infrastructure as code techniques and knowledge will need to be gained for the migration to be successful.

Architecting applications to run in the cloud differs too with scale out approaches being far more common than traditional scale up. Data warehousing techniques look a lot different, rather than large data crunching applications doing all the work, you're more likely to find smaller services being stitched together with queuing systems like Amazon Web Services Simple Queue Service or Kinesis.

Skill gaps can be filled by external consultants and teams, however [dragons can lie](https://www.madetech.com/blog/enterprise-lacking-skills-required-for-cloud-migration) within this solution. System Integrators aren't always as familiar with modern cloud practices as they claim, and often upskilling an existing workforce will pay off in the longer run.

By breaking down the migration into smaller pieces, your teams can build experience moving smaller pieces across to begin with, building confidence and knowledge as they go.

## Cloud migration isn't a one size fits all

Though it may be tempting to see a cloud migration as a lift and shift operation, moving your existing applications to the cloud, but in reality it's a little more nuanced than that. In fact, tackling a cloud migration in a large programme of work in such a fashion is risky, unlikely to provide business value, and perhaps even worse if the migration succeeds, you may end up extended the shelf life of legacy systems.

Understanding which of your applications are mission critical and identifying goals to provide new business value through them will help you decide an approach to migrating that makes the most of cloud.

Understanding the cloud readiness of your existing application estate, the readiness of your organisation, and technical readiness of your team will help you identify blockers that will need to be tackled before you begin migrating.

We'd like to invite you to share your questions about cloud migration with us. Tweet us on [@madetech](https://twitter.com/madetech), or get in touch with myself directly on [luke@madetech.com](mailto:luke@madetech.com).

