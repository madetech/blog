# Pros & Cons of Ruby On Rails

Here at [Made Tech](https://www.madetech.com) we're big fans of [Ruby](https://en.wikipedia.org/wiki/Ruby_programming_language) and use [Ruby on Rails](https://en.wikipedia.org/wiki/Ruby_on_Rails) for most of our web applications. Over the years we've had countless conversations about the pros and cons of Ruby and the reason we favour it over languages like [PHP](https://en.wikipedia.org/wiki/PHP), [Python](https://en.wikipedia.org/wiki/Python_programming_language), [NodeJS](https://en.wikipedia.org/wiki/Node.js) or [GoLang](https://en.wikipedia.org/wiki/Go_programming_language). 

In this article, I want to take you through some of these reasons and explain why we think Ruby is a fantastic choice for a modern web application. 

It is incredibly difficult to succinctly articulate the differences between programming languages. There are literally thousands of different languages, which have evolved over years and are influenced by one another's ancestors. You've only got to take a look at the fantastic evolution diagram (below) to see the incredible ecosystem of programming languages available to engineers. 

[![alt text](http://calvinx.com/wp-content/uploads/2012/07/evo-prog-lang.png "Evolution of programming languages")](http://calvinx.com/wp-content/uploads/2012/07/evo-prog-lang.png)

All programming languages have their quirks and army of advocates who will refute any negativity about their language of choice. This can make it incredible difficult for non-programmers to understand the differences between programming languages and the impact a poor language choice can have on a project. 

In the past, we've seen this result in non-technical customers insisting on using a language they were familiar with (i.e. they had have heard of), rather than selecting the language which was best for the project. In a sense, the language which had the most 'marketing', got selected. *As an aside, we see this happen frequently when people are selecting CMS systems like Drupal too.*

## Programming Languages as Cars
If you're a non-programmer, then a useful analogy is to think of programming languages as being a little bit like cars; Some cars are slow and clunky, yet incredibly reliable. Some are ugly and difficult to drive, yet parts are cheap and plentiful. Others are fast and exciting, but dangerous to drive and expensive to service. 

It wouldn't make sense to take part in a Formula 1 race, whilst driving a Ford Fiesta; and it wouldn't be cost-effective to commute into the office in a McLaren F1. So, if you want your project to run smoothly, then you need to select the most appropriate programming language for the road ahead.

All of our engineers are Polyglots (proficient at programming in multiple languages), so we feel like we've got a good grasp on the pros and cons of many different languages and find Ruby really shines as a general purpose programming language. 

It's worth noting that the software engineering changes rapidly and we expect that within a few years there will be an alternate language / framework, which is more suitable for our needs. (There are a number of candidates on the horizon at the moment, but only time will tell if they prove to be viable long-term options.)

Here's our take on popular programming languages and their car equivalents: 

| Language      | Vehicle             | Reason                                                                          |
| ------------- | :-------------: | :-----------------------------------------------------------------------------  |
| GoLang        | Tesla           | The future, but want somebody I know to buy one first                           |
| Haskell       | Batmobile       | Looks awesome but you'll never figure out how to drive it                       |
| Java          | Hummer          | Uses way more resources than is strictly necessary                              |
| Perl          | Classic Mini    | A classic that has influenced many cars, but not practical for 2015             |
| PHP           | Fiat Multipla   | Ugly, nobody wants to be seen driving this                                      |
| Ruby          | Smart Car       | Practical design. Will get you around the city fast, but not great on motorways |
| Python        | VW Golf         | Solid. Reliable. Middle of the road.                                            |
| NodeJS        | Bicycle         | No licence required. An everyday vehicle for everyone.                                                           |
| .NET          | Zipcar          | Rental. Your car belongs to somebody else                                       |


##Benefits of Ruby on Rails? 

So why Ruby on Rails? We find Ruby provides us with a combination of the best tooling, better quality code libraries and a more pragmatic approach to software. Plus, the ruby community tends to have a higher calibre of engineer, who favour [responsible development](http://www.slideshare.net/TSundberg/the-responsible-developer) over the gun-ho approach that can be seen in other communities.

* **Tooling** - Rails provides fantastic tooling that helps you to deliver more features in less time. It provides a standard structure for web apps, where all the common patterns are taken care of for you. 

* **Libraries** - There's a gem (3rd party module) for just about anything you can think of. They are all publicly available and searchable through https://rubygems.org/. 

* **Code Quality** - Generally, we find the quality of third party Ruby code to be significantly higher than their PHP or NodeJS equivalents. 

* **Test Automation** - The Ruby community is big in to testing and test automation. We believe this is incredibly valuable in helping to deliver good quality software and is one of the reason the Ruby libraries are so great. 

* **Large Community** - Pretty much every major city in the world has a Ruby community that runs regular meetups. It's one of the most popular languages on social coding site Github.  

* **Popular in The Valley** - History has shown that technology that's been popular within Silicon Valley has gradually been adopted across the world. If you look at the big startup successes of recent years, such as Airbnb, Etsy, GitHub & Shopify - they are are all on Ruby on Rails.

* **Responsible Developers** - You tend to find Ruby developers are more closely aligned around the the rules of responsible development. If you start small, communicate well, tackle vertical slices, write simple code over smart code, share ownership etc, you tend to find your project ends up in better shape.

* **Productivity** - Ruby is an eloquent and succinct language, which when combined with the plethora of 3rd party libraries, enables you to development features **incredibly** fast. I would say it's the most productive programming language around.

* **Next Generation** - Ruby on Rails seems to be the language of choice for a number of the popular online code schools, such as [Makers Academy](http://www.makersacademy.com/), [Steer](https://www.steer.me/) and [CodeCademy](https://www.codecademy.com/). This should mean an increase in talented programmers joining the Ruby community over the coming years. 
 
##Disadvantages of Ruby on Rails? 
Of course Rails does have have its disadvantages and it's only fair that we share those in this post. 

* **Runtime Speed** - The most cited argument against Ruby on Rails is that it's "slow". We would agree, certainly when compared to the runtime speed of NodeJS or GoLang. Though in reality, the performance of a Ruby application is incredibly unlikely to be a bottleneck for a business. In 99% of cases, the bottleneck is going to be elsewhere, such as within the engineering team, IO, database or server architecture etc. When you get to a significant enough scale to have to worry about Rails runtime speed, then you're likely to have a incredibly successful application (think Twitter volume) and will have many scaling issues to deal with. 

* **Boot Speed** - The main frustration we hear from developers working in Rails is the boot speed of the Rails framework. Depending on the number of Gem dependencies and files, it can take a significant amount of time to start, which can hinder developer performance. In recent versions of rails this has been somewhat combat by the introduction of (Spring)[https://github.com/rails/spring], but we feel this could still be faster. 

* **Documentation** - It can be hard to find good documentation. Particularly for the less popular Gems and for libraries which make heavy use of mixins (which is most of Rails). You'll often end up finding the test suite acts as documentation and you'll rely on this to understand behaviour. This isn't itself a bad thing, as the test suite should be the most up-to-date representation of the system, however, it can still be frustrating having to dive into code, when sometimes written documentation would have been much quicker. 

* **Multithreading** - Rails supports multithreading, though some of the IO libraries do not, as they keep hold of the GIL (Global Interpreter Lock). This means if you're not careful, requests will get queued up behind the active request and can introduce performance issues. In practice, this isn't too much of a problem as if you use a library that relies on GLI, you can switch to multiprocess setup. The knock-on effect of this is your application ends up consuming more compute resources than necessary, which can increase your infastructure costs.

* **ActiveRecord** - AR is used heavily within the Ruby on Rails world and is a hard dependency for many of the RubyGems. Although we think it's a great design pattern, the biggest drawback we see is that your domain becomes tightly coupled to your persistence mechanism. This is far from ideal and can  lead to bad architecture decisions. There are many ways to work around this, some of which are included in this [7 Patterns to Refactor Fat ActiveRecord Models](http://blog.codeclimate.com/blog/2012/10/17/7-ways-to-decompose-fat-activerecord-models/) article. We would like to see Rails become less reliant on ActiveRecord.

##Conclusion

There are use-cases for pretty much every programming language referenced and you'll find advocates of them all. If you are delivering a new application for the web, then we would advise you to develop it in Ruby, Python, NodeJS or GoLang. 

The other languages will still get you you from A-B, but at the end of the day, who wants to be seen driving a Fiat Multipla? 