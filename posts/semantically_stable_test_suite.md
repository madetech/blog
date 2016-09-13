# Semantically Stable Test Suites

## Code coverage

When we run a test suite in most languages, we can also generate reports with percentage of code coverage.

This is really great, because it allows us to see in a metric the reliability of our test suite.

The problem with code coverage is that it is a *lie*. This lie forms the reason why you cannot trust this metric. It is also the reason why you should not fail the build because of this metric.

### Uncovering the lie

Remove all the assertions from your test suite, now rerun it. Your code coverage metric will be **unchanged**.

What does this mean?

Simply put, it means you cannot trust the Code Coverage metric.

##  Semantic Stability

A semantically stable test suite, is a test suite that fails (given that there are two states of build status: pass or fail) when any semantics of the production code that it is covering is changed.

What this means in practice is that every character of production code *has a reason to be there*, and that changing any aspect of the code will cause the test suite to fail.

Of course, the production code could be modified to retain it’s semantics, but be implemented in a different way. 

As an example it should be possible to swap out the disk scheduling algorithm used by a disk driver from first-come first-serve (FCFS) to shortest seek time first, and not impact the semantics (the fundamental useful behaviour) of the system under test. Another example could be swapping out using a merge sort for a quick sort.

## Semantic stability as a metric

Luckily there are tools available to measure semantic stability, called **mutation testing tools**. Similar to code coverage, these tools provide a % of lines which when mutated were detected by the test suite (the terminology for this in the mutation testing world, is that the test suite kills the mutants on those lines).

## Achieving 100% semantic stability

### TDD

Following the test-first discipline of TDD, strictly, whereby no single line of production code is written without first watching a test fail for that change to be made, produces semantically stable test suites by default.

### Mutation testing tools

It is possible to use mutation testing tools, and a lot of time, to create semantically stable test suites. 

The method behind this approach would be to write assertions in your test suite, for all elements of your code that can be mutated without being killed by the test suite.

## Who needs semantic stability anyway?

Iff code coverage is an asymptotic goal then it is implied that semantic stability of your code base is also an asymptotic goal.

In well-designed systems uncovered lines tend to not change, they tend to be calls to the system, external systems, libraries or general IO. They tend to be *low-level details*.

### The customer cares about high-level policy.

High-level policy is the business logic. It is the logic which in an accounting system, calculates tax on an invoice, and knows about double-entry accounting. As such it is the application code that both you and the customer you care about. 

In this world of high-level policy, we do not concern ourselves with low-level detail like databases, and web-frameworks. These are things that only programmers care about, these details only get in the way of describing the problem domain at hand.

Really your customer cares about two things: 

a) that they can request changes to high-level policy, and that this can be done cheaply.
b) that the system works the way they currently have described they want it to

The best way to make it possible to cheaply change high-level policy is to ensure you have tests. However it becomes significantly cheaper to ship changes to high-level policy when you have a semantically stable test suite.

Secondly, the best way to ensure that the system works is surprisingly: to write tests. You cannot be certain that a system works 100% as you expect it to, unless your test suite is semantically stable. 

## Software should be soft

Fear holds back practices like boyscouting. Fear of changing the production code ultimately stems from distrust of the test suite. 

The fundamental role of software is to be soft. It is supposed to be cheap to change, and remould to perform new behaviours while maintaining the old behaviours that are already depended upon. To that end I would say it is very rare for a customer to ask to remove a feature from a system. The common use case is to extend and build upon the features that are already there.
