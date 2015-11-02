# Planning an Agile backlog 
Most Agile methodologies work in small independant units of work - often called User Stories. Coming up with these is it's own challenge, and one I plan to tackle in a future post. Today though I want to discuss how to determine if a User Story is valuable, and from there I'll outline a method for turning a list of disparate stories into a working backlog for commencing an Agile project.

##Three types of value
The [Kano Model](https://en.wikipedia.org/wiki/Kano_model) talks about five types of value. To keep things simple though I'm only going to cover three:
Must-have/Basic Needs: Users will think less of you product if you don't have these features.
Performance needs: The more of these you have, and the better they are implemented: the better your product is received.
Exciters/Luxury needs: New/novel improvements or optimisations, the presence of which will exponentially improve user perception.

##Group by value
Given our initial backlog of stories attained at a user workshop, we'll first aim to classify our User Stories into these three categories. In my experience about ninety percent should fit into these three groups (and the remainder likely into the remaining two). We can use these broad brush strokes to give us an initial sense of the project's size. In general:
* We should implement as many Basic Needs as is feasible
* We should aim to complete as many Performance Needs as we can afford
* We want to include a few Luxury needs, to increase user experience, and for market differentiation.

A similar method of prioritisation is to use MoSCoW (Must, Should, Could, Won't) to do this first pass, I Prefer to use Kano though. MoSCow can bring subtle cognitive biases to the table, as many people familiar with it have the mistaken notion that anything that's not a 'Must-have' won't get built. 

##Bucketing by Theme
We've now bucketed your features by need, it's also useful to now do so by theme, e.g. in the context of an eCommerce store: checkout, user accounts, product information pages are three (of likely many more themes). The key thing to notice is that these are orthogonal to our needs column above, we might decide that being able to purchase at all is a must-have, whereas accepting the latest crypto-currency is probably an Exciter at best; both would probably fall into a checkout/payment theme though. It's helpful to group features in the same value and theme together, so that during development the engineering team will work on them sequentially. In practice this will make development more efficient as the team won't be constantly jumping between disparate parts of the codebase.

##Identify a walking skeleton
Now you want to run through your basic needs, with the aim of pulling out a core 'Walking Skeleton' or MVP. This is the absolute minimum of features that ties your application together end to end, and it may be helpful to work with your engineering team for this excercise. The idea is that this is going to build a very rapid prototype for the first sprint or two. This forms a stable foundation which we can build on in later iterations - putting the meat on the bones as it were. 

Try and imagine the walking skeleton for a car - for the sake of argument lets assume we don't need to worry about passing any kind of legal/safety requirements - this is just a prototype. Our must haves are propulsion, steering, and somewhere to sit, plus the absolute minimum needed to attach this all together - a basic chassis. The gearbox can wait and windows are an unnecessary extravagence at this point. That's not to say that we won't add either of these things later, just that for now we'll be happy with a golf buggy, we'll use subsequent iterations to turn it into a Ferarri, or a Prius.

##Identifying biggest risks
Every project has risk, and most of the time the risk is manageable. Most projects will have some inbuilt assumptions though, and the project outset is a good time to try and figure out what these are. Perhaps there's a new API you're relying on but have never used, or maybe you're unsure if there's a market for what you're selling. It's absolutely not worth the time to fully implement these things at the outset, as this may take many weeks, and we're more interested in building a proof of concept at the moment. However it's definitely beneficial to set aside a day or two to get some reassurance on the biggest unknowns - the stuff that will sink the project if our assumtions prove false.

##Triage your remaining must haves
These will form the main bulk of the application, and are things that you or your users would consider your product incomplete without. These are usually fairly obviously fundamental to function, and will include things like product listings on an ecommerce site (though likely not search). Reviewing your must-have's is a great opportunity to really challenge your assumptions - do we need this because the site won't function without it? Or because most of the competing solutions have this feature? Streamlining your feature set early on will give you the greastest flexibility for change later.

##Performance needs
These are things which improve a users experience, but your user demographic is going to massively impact what fits inside this category. If we're trying to build a novice image editing tool, we should be wary of building something too complicated for our users, as that will alienate our market. We don't want to build Photoshop if our users only needs MS Paint. Also beware of dimishing returns with your performance features, adding your first will add a lot of perceived value to your product, but adding a twentieth will add much less.

##What are your key exciters?
Similar to above, you don't wont to go too overboard with these, especially at the expense of core needs. However, exciters are what will differentiate you from your competitors, so it's defintely worth adding a couple of well considered such features. It's hard to think of a big tech success which hasn't had a well executed hook (note that 'first to market' is rarely a sufficient hook). Google had Pagerank; Candy Crush added a lives system to a well trodden 'match-three' formula to keep users from burning out; and shaving company Harry's had a [killer referral scheme](http://fourhourworkweek.com/2014/07/21/harrys-prelaunchr-email/) to drive explosive growth. 

##Embrace change - but prepare for it
The most important part of any project, and the hardest to account for in practice. At the project outset you know less about the project than you will at any point in the future, yet so often is it at the beginning when most expectations are set. If you've been though all the above steps, you hopefully have a pretty solid picture of what you're going to build, but this is all based on imperfect knowledge. I can guarantee that there are features and assumptions that you haven't thought of, and those which are necessary are going to take a huge bite out of your plan. Better to plan for this ahead of time - not by trying to identify every potential change, but by carving out a chunk of your timeline to afford an opportunity to pivot if required.

##To sum up
This isn't intended to be a magic wand for all projects, nor is it a hard and fast rule, but I recommend that newcomers to Agile try and break up their first project using the following proportions. If you're a newcomer in a nascent market you might want to forego exciters in favour of getting the core journey right. On the other hand if you're entering a crowded space you might want to invest heavily in luxury features to better stand out from the crowd. 

* Walking Skeleton: 5-10% of project
* Spike out the big risks: 0-10%
* Flesh out the core features: 30-70%
* Key performance features: 10-30%
* A couple of exciters: 10-30%

Leave at least 25% for stuff you haven't thought of yet!
