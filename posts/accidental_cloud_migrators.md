# How we accidentally became cloud migrators

When coming up with an explanation of our cloud migration heritage for my talk at Red Hat Forum the phrase "accidental cloud migrators" came to mind. You see we didn't set out to help organisations move workloads to the cloud but nevertheless we've found ourselves helping organisations modernise and migrate. On reflection, I think accidental cloud migrations are the best kind of migration, let me explain why.

We are a company of software engineers of mostly web based apps, platforms and microservices. We wouldn't dream of building a greenfield system on-premise or in a datacenter, it would take too long and it's too costly. We can orchestrate and test cloud infrastructure with the tool we know, code.

If you look at the world from our perspective for a moment, why would you physically go to a datacenter and install hardware when you can provision in the cloud and deliver value sooner? Going one step further, why would we use an admin interface to configure anything in AWS when we can use code instead? Manual steps lead to human error. From the early days of cloud we've been writing code to provision and orchestrate our infrastructure with tools like Ansible.

We happen to be early users of Amazon Web Services with our team using it commercially even prior to Made Tech coming into existence 9 years ago. It's just a default tool of choice for us whereas its a game of catch up for older organisations. I suppose this is why we hear about big 2 year programmes of work to lift and shift legacy infrastructure to the cloud. "Let's get to the cloud and quick before we are disrupted," businesses cry.

## Our journey into legacy applications

When Made Tech started out we focussed mainly on greenfield custom applications. Sure, we integrated with some older systems but for the most part the issues of legacy weren't something we had to deal with. This was because the majority of our customers back then were startups wanting to get a product to market in 100 days. This really helped shape our lean thinking and approach that we continue to use to this day.

Our approach and mindset seemed to appeal to various CTOs and Heads of IT in more established startups where we began to work along side existing engineering teams. Whilst in-house engineers were bogged down fighting fires, we would be delivering value for the business. Helping the in-house engineers with their fires would usually end up becoming a priority. We would share practices like continuous integration and delivery, automating BAU chores, acceptance testing, pair programming, variants of agile, etc. to help improve effectiveness, quality, and in the end, happiness of teams.

> Legacy isn't limited to applications. Process, culture and decisions are all legacy too.

The more established startups had their fair share of legacy applications albeit built with relatively new technology and still mostly with a cloud first approach. Good practice was still missing though with cloud infrastructure configured by hand, manual or semi-manual deployments, a lack of automated testing and so forth.

As we began to work with larger and larger organisations, we began to realise a few of things:

1. Legacy can be very complex and is often a political issue
2. Our lean and agile approach could probably benefit larger and older organisations
3. It would be tough job to adapt ourselves to those organisations

We began to see on-premise and datacentre infrastructure more frequently. Mix that and the politics of global organisations and it was clear to see why things are so hard to change.

It was at this point we were realising that technology is only part of the problem. We were learning that process and culture were hugely important factors that needed to change too. Legacy isn't limited to applications. Process, culture and decisions are all legacy too.

## Cloud migration as a side effect

The common theme among our customers nowadays is that their business is hindered by legacy systems and technologies. One such legacy system we see time and time again is the proprietary ERP at the centre of a business. It's a common issue with ecommerce and supply chain businesses. Traditional ERPs are expensive, often requiring on-premise servers and they limit a business' ability to change business process. The last point is a often a huge one, businesses will either force their processes to fit the ERP or will default back to paper solutions or other workarounds.

We've helped a number of businesses move away from legacy ERP, purchasing and warehouse systems. Rather than focus simply eradicating legacy, which is a fallacy by the way, we put together a roadmap that explains the business value modernisation and migration will bring. We usually list 4-5 goals per roadmap to measure ourselves against:

- Onboard new clients easily and be able to handle more business
- Reduce manual work and paperwork for more efficiency
- Team and clients can trust the quality and granularity of data
- Work with a greater number of suppliers & partners

These goals speak nothing of a cloud migration or removing legacy systems. They are goals, that if met, will provide new value to the business in the form of efficiency, trust and scale.

All of these projects did end up being implemented in the cloud or at least in some hybrid form. Why continue to pay outsourced IT technicians to keep servers running in your office? Why require remote workers to VPN into your office connection rather than VPN directly into a cloud setup? Reliability is a huge issue when talking about on-premise, as well as it being slow to change and expensive.

Cloud based solutions. Modern architectures and approaches. Change to culture and process. All must be implementation details of trying to provide more value to a business.

## Migrations driven by business value

It's in this sense that we are accidental cloud migrators. We've grown our skills around working with on-premise and datacentre legacy systems, working out how to transition businesses iteratively and therefore safely to the cloud without ever directly trying to sell cloud migration as a concept or set cloud migration as a goal.

We continue to "accidentally" migrate our customers to modern infrastructure in the cloud but only where we can prove it will provide business value. We do it because we believe this is the best kind of cloud migration.
