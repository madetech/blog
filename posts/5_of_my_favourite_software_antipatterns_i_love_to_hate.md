# 5 Of My Favourite Software AntiPatterns That I Love To Hate

- Accidental complexity
- Dependency hell
- Catch me if you can
- Blind faith
- Abstractions of deceit
- Conclusion

  **Software anti-patterns is a well covered topic, but I thought I would highlight some of the ones that I have encountered most frequently.
  These may seem obvious and even at times innocent looking but make no mistake, they are sinister and will sabotage your efforts to add features to a codebase.
  I have made up my own names for some of these more specific anti-patterns.**

## Accidental complexity

  I would consider this a blanket anti-pattern which hosts an array of other anti-patterns.

  What is special about accidental complexity is it's ability to grow exponentially.  One bad decision early on could trigger a bunch of (wrong)
  defensive decisions later on.

  New anti-patterns start surfacing like 'Reinventing the square wheel'.  A popular way for this to happen is when developers make the decision to solve a
  certain problem using their own code, as opposed to using tried and tested solutions that already exist.  Let's create our own CMS!
  You will be too focussed on trying to fix your code to consider the bigger picture.  The 80 / 20 rule comes into play here.

## Dependency hell

  We've all been there.  Try and add a specific version of a gem to your project, run bundle install and be faced with a wall of red text complaining
  about versions being incompatible.

  Also when dealing with external systems (which has become ever more popular as systems become decentralised), they might get into a tug of
  war over what they consider correctness of data.  Your app sits in the middle and has to keep both happy.
  Accidental complexity lies in wait, ready to complect your code.

  A example of this that I ran into recently is where I had Salesforce vs Carmen expecting different names for the same country.

  Salesforce would only accept 'Korea', and Carmen would only accept 'Korea, Republic of'.  It is not hard to solve without inheriting accidental
  complexity.
  A way to solve this is to create an intermediate representations of the data housed in your application itself.
  Good luck to the next developer that will inherit the codebase to figure out what exactly is going on.

## Catch me if you can

  Have you ever looked at a codebase to try and find the place to make your change, only to be thrown down a never ending rabbit hole of abstractions?

  I was unable to find an anti-pattern to define exactly this, so I just named it myself.
  It also falls under the all encompassing Accidental complexity anti-pattern like most others do.

  I am a huge fan of abstractions and small methods, but have hunted through some frameworks where the search just never seems to stop.
  This can be a result of pre-mature optimisation, or just making things too general before it is needed.
  It may be designed to deal with a huge amount of complexity where it will never been needed.

  Without some sort of IDE functionality to navigate between the files you are left stranded.

## Blind faith

  Friday afternoon, everything is going great, you push your commit to production, check New Relic, and all hell breaks loose.

  Your fix has broken a bunch of other code, and your customer's shop is now offline.
  All you can hear is money falling on the floor.

  It takes 30 minutes to run your test suite locally.  That is a lot of time for the website to be down.
  You cannot roll back using your awesome blue/green deployment system because your commit has changed the database schema (doh!)
  You frantically revert your commit, and push it back into the master branch.

  Jenkins starts building your project and your test suite FAILS.  You have introduced more bugs than there used to be in the first place.
  You are not moving forward, you are moving backwards at a rapid pace.
  The only advice I have in this situation is to remain calm.  Your ability to solve the problem only decreases when you start getting stressed.
  Formulate a plan before just trying to solve the problem on the spot.

## Abstracions of deceit

  Also not a formal anti-pattern but definitely a descendant of Accidental complexity.

  There is a huge difference between reading:

  **convert_price**

  and

  **convert_base_price_to_requested_currency**

  It is good to introduce code [seams](http://www.informit.com/articles/article.aspx?p=359417&seqNum=2) as a way to add new functionality if your
  abstraction is not accurately named, it can be worse than having no abstraction at all.

  On the other side of this is the 'Too long and verbose names' anti-pattern which I consider way less harmful this anti-pattern.
  It may hinder your ability to scan the codebase quickly, but atleast once you read it, you will have a clear understanding of what it aims to
  achieve.

## Conclusion

  Naming is hard but it is good to label things so that they can be easily discussed.
  Be on the lookout for anti-patterns that you may come your way, and flag them by name as soon as you recognise them.
  It also facilitates discussions when you can reference something by name, as opposed to explaining what you mean every time.
