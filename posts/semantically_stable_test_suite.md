# Semantically Stable Test Suites

## Code coverage

When we run a test suite in most languages, we can also generate reports with percentage of code coverage. These reports aren’t all they are cracked up to be.

The way that testing tools generally create these reports is by analysing which lines of production code were executed while the test suite was running. It then can, if you want it to, output a report on how many lines/methods/files were covered by your test suite. 

This coverage percentage is generally used as a reliability metric of a given test suite. Great! Since we have a metric, we can now fail the build when the code coverage is too low… 

Unfortunately it is not as simple as that. 

The problem with code coverage is that it is a *lie*. This lie forms the reason why you cannot trust this metric. It is also the reason why you should not fail the build because of this metric.

### Uncovering the lie

Remove all the assertions from your test suite, now rerun it. Your code coverage metric will be **unchanged**.

What does this mean?

Simply put, it means you cannot trust the Code Coverage metric.

##  Semantic Stability

A *semantically stable* test suite is one that fails (given that there are two possible final states: pass or fail) when any semantics of the production code that it is covering is changed.

What this means in practice is that every aspect of the production code *has a reason to be there* and that changing any aspect of the production code will cause the test suite to fail.

Of course, the production code could be modified to retain its semantics, but be implemented in a different way.

As an example it should be possible to swap out a merge sort for a quick sort, and not impact the semantics (the fundamental useful behaviour) of the system under test. As a potentially more complicated example, one could also swap the disk scheduling algorithm used by a disk driver from first-come first-serve (FCFS) to shortest seek time first.

However it could also be much more subtle: for example, a semantically equivalent version could be one which makes it a little easier for the next programmer to understand, or easier to extend. 

## Semantic stability as a metric

Luckily there are tools available to measure semantic stability, called **mutation testing tools**.

Mutation testing tools generate many versions (mutants) of your production code, with very small changes (mutations) made in order to attempt to make your test suite *not catch* those changes. Similar to code coverage, these tools provide a % of lines which when mutated cause the test suite to fail; this is a good thing! 

When this happens we have semantic stability. The terminology for this in the mutation testing world is that the test suite kills the mutants.

## Achieving 100% semantic stability

### Test Driven Development

Following the test-first discipline of TDD strictly, whereby no single line of production code is written without first watching a test fail for that change to be made, produces semantically stable test suites by default.

### Mutation testing tools

Alternatively it is possible to use mutation testing tools to create semantically stable test suites. 

The method behind this approach would be to write assertions in your test suite, for all elements of your code that can be mutated without being killed by the test suite.

The problem with this approach is that it is time consuming, due to the fact that the tooling is slow. 

## Who needs semantic stability anyway?

Both the percentage of semantic stability of your test suite, and the percentage of code coverage are asymptotic in nature with respect to the cost. In that it is increasingly more difficult to achieve as you approach 100%, and it is not usually practically feasible to achieve 100%. 

In well-designed systems uncovered lines tend to not change, they tend to be calls to the system, external systems, libraries or general IO. They tend to be *low-level details*.

It is possible to push the areas of low code coverage to the outermost extremes of your application. Treating them instead as details that get in the way of shipping working, high-value software.   

### The customer cares about high-level policy.

High-level policy is the business logic. It is the logic which in an accounting system calculates tax on an invoice, and knows about double-entry accounting. As such it is only this application code that both you and the customer care about. 

In this world of high-level policy, we do not concern ourselves with low-level detail like databases, and web-frameworks. These are things that only programmers care about, these details only get in the way of describing the problem domain at hand.

Really your customer cares about two things: 

a. that they can request changes to high-level policy, and that this can be done cheaply.
b. that the system works the way they currently have described they want it to

The best way to make it possible to cheaply change high-level policy is to ensure you have tests. However it becomes significantly cheaper to ship changes to high-level policy when you have a semantically stable test suite.

Secondly, the best way to ensure that the system works is, surprisingly, to write tests. You cannot be certain that a system works 100% as you expect it to, unless your test suite is semantically stable. 

## Software should be soft

Fear holds back practices like refactoring to remove technical debt. Fear of changing the production code ultimately stems from distrust of the test suite. 

The fundamental role of software is to be soft. It is supposed to be cheap to change and remould to perform new behaviours while maintaining the old behaviours that are already depended upon. To that end I would say it is very rare for a customer to ask to remove a feature from a system. The common use case is to extend and build upon the features that are already there.
