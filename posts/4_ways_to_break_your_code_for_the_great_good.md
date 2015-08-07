 4 ways to break your code for the great good
 ---------------------------------------------

 Mutation testing
 Fuzz testing
 Fault injection
 Bebugging

 Software development is all about managing complexity.  We employ tools to help us with this such as software testing.
 This however raises the question of Quis custodiet ipsos custodes? or Who will guard the guards?

 Below we will see some techniques for improving test coverage in a program.

Mutation testing
-----------------

Mutation testing is a form of test coverage that is designed to evaluate the quality of your test suite.
By modifying your production code like changing an || to an &&, it would expect at least one test to fail.
If a test fails, you have successfully killed the mutant.
Mutants that survive can be analyzed and new test can be written for them.

There is a caveat to mutation testing, which I believe has prevented it from becoming a practical everyday tool.

The equivalent mutants.

It is possible for the mutant to modify your program in such a way that the behaviour is still exactly the same.
Your tests would never fail and the mutant will always survive.

This problem has been subject to a lot of research and experimentation.

Another popular form of program mutation is Statement deletion.
This too may point out interesting edge cases where you may want to increase test coverage.

  Testing with ruby
  ===================
  You can test your rails application quite easily, right now with the awesome Mutant Gem.
  https://github.com/mbj/mutant

  Here is a list of mutants that you can use to mutate your code.
    https://github.com/mbj/mutant/tree/master/meta

Fuzz testing
-------------

With Fuzz testing, the goal is to get your program to fail by bombarding it with random data until it does.
Division by 0 errors, out of range values .etc will all be highlighted when this is run.
This is also form of black box testing that indicates the long term quality of your tests.
This is quite popular for testing security systems to discover 'trust boundaries' before anyone else does.

This form of testing has been around since the 80s, and was even used by Apple to test MacPaint.
You want your program to be aware of exceptions and not just carry on given invalid input.

Chances are that this form of testing will expose oversights and defects that humans are unable to find.

Fault injection
----------------

This form of testing aims to follow error code paths through your application that might otherwise rarely be triggered.
It has been around since the 70s, and is also used on hardware.
In those days people would do things like short out connections on circuit boards, or even bombarding specific parts of the circuit with
radiation.

2 primary techniques in the software world for testing this are compile-time injection and runtime injection.
The goal is to try and reproduce similiar faults that may have been accidentally added by programmers.
Rather than modifying code as we saw with mutation testing, this adds code to introduce the fault.

Bebugging
----------

This is another way to measure test coverage of a system, and has also been around since the 70s.
Common errors are introduced into a program, and it is up to the developer working on the system to find them.

Rate of detection and remaining undetected bugs are used to measure how well the code is covered by tests.
