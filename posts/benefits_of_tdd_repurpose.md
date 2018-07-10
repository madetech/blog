# Test-Driven Development: 
# A waste of time or the best thing since sliced bread?

[Test-Driven Development](https://en.wikipedia.org/wiki/Test-driven_development) (TDD), is a software development process that relies on the repetition of a very short development cycle: requirements are turned into very specific test cases, then the software is improved to pass the new tests, only. This is opposed to software development that allows software that is not proven to meet requirements to be added.
So is TDD a necessary evil?
Necessary yes; evil no. Although it can feel like it, TDD needs to be reframed away from feeling like a chore and instead be looked at as the right thing to do. That way, when the inevitable pressure comes in from clients and employers alike, you’ll be able to communicate the benefits of TDD and ensure your team gets adequate time for completing it. 

At Made Tech, we use TDD when writing our feature specs. We use tools most commonly applicable to unit tests for our feature tests too, such as RSpec with Capybara helpers, rather than things like Cucumber, which are often associated with Behavior-Driven Development or BDD (that said, you can still use Cucumber for feature specs and TDD). And we’ve noticed a lot of positive effects when the time is taken to do TDD so we wanted to share them. 

## Target practice

You're more productive while coding, and TDD helps keep that productivity high by narrowing focus. How? Well first, if you consider the features you want to create and create tests to ensure they are included in your work, you make sure you will meet the customer’s criteria. It also forces you to think about smaller chunks of functionality at a time rather than the application as a whole. Once the test has failed, you can then incrementally build a passing test, rather than trying to tackling everything in one go which may result in more confusion and bugs, and therefore a longer development time overall.


## Going public

When writing a code class, you have to think about the public versus private methods; what can be reused and what shouldn’t be. Writing the test ensures the public methods are trialled first without worrying about the inner workings of the project resulting in better, more sensical code. 

TDD will give you a clearer perspective on what can be made public and what can be kept private. This will avoid a situation where code has been released publically when it should have remained private, thereby, creating extra work for something that was intended to be in an internal class.

## Mock trial

If your code will have dependencies, TDD allows you to mock them out without worrying about what’s going on behind the scenes. This also means the dependencies you mock may be faster when running the tests without bringing additional dependencies to your test suite in the form of filesystems, networks, databases etc. Two birds one stone.

## Better safe than sorry

Once a test passes, it's safe to refactor your code. Occasionally however, you’ll find yourself working with code authored by someone else and tests won’t have been done. The decision then rests with you to continue or go back and undertake TDD. If you want to be in a better position to refactor or add new functionality without breaking existing capabilities, then TDD is the best thing to do; write a test that covers as much as you can, and then proceed.

## Got the bug

Earlier we explained that communicating the benefits of TDD to a client means getting the time you need to run the tests. One of the reasons for doing this is TDD creates more tests and increases test run times; ‘bad’ in the short-run, but you need to play the long game. Why? Because better code coverage at the start saves time that would be spent defining and fixing bugs at the end. 

## Higher rate of return

Obviously when compared to not writing any tests, the initial cost of TDD is higher. On the whole however, projects that don't have a TDD foundation usually end up costing more due to a lack of any or suitable test code coverage, making them more susceptible to bugs and issues, which cost more to fix in the long-run.

Not only does TDD save time on fixing bugs, the cost to change functionality is reduced because the tests act as a safety net to ensure any subsequent changes won't break existing functionality.

## Track record

Tests can serve as documentation to a developer. If you're unsure of how a class or library works, go and have a read through the tests. With TDD, tests usually get written for different scenarios, one of which is probably how you want to use the class. So you can see the expected inputs a method requires and what you can expect as outcome, all based on the assertions made in the test.

## Final thought
It’s key to remember that TDD is never a waste of time because the benefits are so many and varied. While it might seem double the work, you have to speculate to accumulate for long-term delivery. 
When writing new code, you’ll either have a list of required features or acceptance criteria that needs to be met. Once you’ve written the failing test, you can proceed to the next stage safe in the knowledge that you haven’t missed anything and that the end result will be solid, thought-through, and most importantly, working well.

