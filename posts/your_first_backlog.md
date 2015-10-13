# Planning yur first Agile project 
#Overview of agile - work on most valuable things first
Most Agile methodologies work, by encouraging small independant bits of work which are in some sense valuable. These units of work are often called User Stories. Coming up with these is it's own challenge, and one I plan to tackle in a future post. What I want to talk about today is what it means for a User Story to be valuable? How can we measure it? How do I take a list of user stories and turn them into a project?

##3 types of value
The [Kano Model](https://en.wikipedia.org/wiki/Kano_model) talks about 5 types of value. For a new software project though we mostly care about the following 3:
Must-be/Basic: Users will think less of you product the more of these that you don't have
Performance needs: The more/better these are the better your product is received
Exciters: New/novel improvements, the presence of which exponentially increases a users opinion of your product

#Grouping similar themes
Using these types of value we can now begin to classify such features, 90% of them will fall into 1 of the three categories. This will form the basis of the early stages of development, which depending on our budget should include most of the must-haves as many 'performance' as we can afford plus a few exciters to gain initial excitement. Note that this is similar to using MoSCow - you're 'Must' category is basically the same in both, but I prefer this method as it gives you a bit more guidance for classifying 'non-must' features. 

#Bucketing
We've now bucketed your features by need, it's probably useful to now do so by theme, e.g. in the context of an eCommerce store: checkout, user accounts, product information pages are three (of likely many more themes). The key thing to notice is that these are orthogonal to our needs coloumn above, we might decide that being able to purchase at all is a must-have, but accepting the latest crypto-currency is probably an Exciter at best! Both would porbably fall into a checkout/payment theme though.

#What is your walking skeleton?
What the absolute minimum of features that ties your app together end to end? This is going to form the basis of the first sprint so you need to think as minimally as possible. This gives us a stable foundation which we can build on in later iterations. Imagine for a moment that we're building a car - For the sake of argument lets assume we don't need to worry about passing any kind of legal requireents - this is just a prototype. Our must haves? Wheels, Steering, Chassis, Engine. The gearbox can probably wait if we're happy just pootling around. Windows are an unnecessary extravagence. That's not to say we won't add either of these things later, just that for now we'll be happy with a golf buggy for now, we can turn it into a Ferarri, or a Prius later on.

#Identifying biggest risks
Next we want to take a moment to look ahead. Every project has risk, but for most the risk is pretty manageable. At the outset it's worth taking the time to investigate the real project killers, perhaps there's a new API you're relying on but have never used. Is there a particularly hairy integration that you're worried about. It's probably not may not be worth the time to fully implement these at the outset, when we're more interested in building a proof of concept than a full featured product. It's almost certainly worth spending a couple of times double checking your assuptions about your 'project killers' - the stuff that if we can't do it is going to sink the project.

#Triage your remaining must haves
These form the main bulk of the application, these are things that you or your users would consider your product incomplete without. This probably includes things like product listings on an ecommerce site (though maybe not search). Reviewing your musts is a great opportunity to really challenge your assumptions - do we need this because the site won't function without it? Or because most of the competing solutions have this feature? Streamlining your feature set early on will give you the greastest flexibility for change later.

#Performance needs
These are things which improve a users experience, but your user demographic is going to massively impact what fits inside this category. If we're trying to build a tool for image editing for novice computer users, we don't want to end up with something too complicated for our users to understand, as that will alienate our target market. We don't want to build Photoshop if our users only needs MS Paint. Also beware of dimishing returns with your performance features, adding your first will add a lot of perceived value to your product, but adding your 20th will add much less.

#What are our key exciters?
Similar to above, you don't wont to go too overboard with these, especially at the expense of core features. However, exciters are what is going to be what differentiate you from your competitiors, so it's defintely worth adding a couple of well considered such feeatures. Most of the big tech successes have all had a 'hook' (and rarely is 'first to market a sufficient hook these days'). Google had Pagerank; Candy Crush added a lives system to an existing formula to keep users wanting more; and shaving company Harry's had a [killer referral scheme](http://fourhourworkweek.com/2014/07/21/harrys-prelaunchr-email/) to drive explosive growth. 

#Don't fear change - embrace it
The most important part of any project, and the hardest to account for in practice. At the project outset you know less about the project than you will at any point in the future, yet so often is it at the beginning when you need to know how long it will take. If you've been though all the above steps, you hopefully now have a pretty solid picture of what you're going to build, but the bad news is that you have imperfect knowledge. I can guarantee that there are obvious features you haven't thought of, and those which are necessary are going to take a huge bite out of your plan. Better to plan for this ahead of time - not by trying to identify them, but by carving out a chunk of your timeline to tackle them when they come up.

#To sum up
This isn't intended to be a silver bullet for all projects, nor is it a hard and fast rule, but I recommend that newcomers to Agile try and break up their first project according to the following proportions. If you're one of the first in a relatively naissant market you might want to forego exciters in favour of getting the core journey right. On the other hand if your entering a crowded market you might want to invest heavily in those same Exciters in order to stand out from the crowd. 

* Walking Skeleton: 5-10% of project
* Spike out the big risks: 0-10%
* Flesh out the core features: 30-70%
* Key performance features: 10-30%
* A couple of exciters: 10-30%

Leave 25% for stuff you haven't thought of yet!
