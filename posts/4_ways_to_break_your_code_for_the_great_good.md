# 4 ways to break your code for the great good

 * Mutation testing
 * Fuzz testing
 * Fault injection
 * Bebugging

Software development is all about managing complexity.  We employ tools like automated testing to guard existing functionality from regression.

This however raises the question of [Quis custodiet ipsos custodes?](https://en.wikipedia.org/wiki/Quis_custodiet_ipsos_custodes) or Who will guard the guards?

Below are some techniques that could point out edge cases in your tests that may have gone undetected.

### Mutation testing

Mutation testing is a tool designed to evaluate the quality of your test suite.
By modifying your program in small ways like changing an || to an &&, it would expect at least one test to fail.
If a test fails, you have successfully killed a 'mutant'.
Mutants that survive can be analysed and new test can be written for them if necessary.

There is one caveat to mutation testing which is the dreaded 'The equivalent mutant'.

It is possible for the mutant to modify your program in such a way that the behaviour is still exactly the same.
Your tests would never fail and the mutant will always survive.

This problem has been subject to a lot of research and experimentation.

Another popular form of program mutation is Statement deletion.
This too may point out interesting areas where you may want to increase test comprehensiveness.

#### Testing with ruby
You can test your rails application quite easily, right now with the awesome [Mutant Gem](https://github.com/mbj/mutant).

Here is a list of [mutants](https://github.com/mbj/mutant/tree/master/meta) that you can use to mutate your code.

### Fuzz testing

The goal of Fuzz testing or Fuzzing is to get your program to fail by bombarding it with random data.
This form of testing has been around since the 80s, and was even used by Apple to test MacPaint back in those days.

Division by 0 errors, out of range values .etc may all be highlighted when this is run.

This form of black box testing can reveal defects in your software in an automated way so that you do not have to try do this manually.
This is quite popular for testing security systems to discover [Trust Boundaries](https://en.wikipedia.org/wiki/Trust_boundary).

Ideally you want your program to respond to exceptions in an appropriate way and not just proceed in an unknown state.

## Fault injection

This form of testing aims to follow error code paths through your application that might otherwise rarely be triggered.

It has been around since the 70s and is also popular in the hardware testing world.

In hardware fault injection they would do things like short out connections on circuit boards, or even bombard specific parts of the circuit with heavy
radiation to see how the overall system copes.

Two primary techniques in the software world for testing this are compile-time injection and runtime injection.

Faults are introduced into the program and these may propagate up the stack to cause further errors within the system boundary.
Faults making it up to the observable system boundary are marked as failures.

## Bebugging

This is another way to measure test comprehensiveness, and has also been around since the 70s.
It is a tool to get an idea of the average amount of bugs that potentially make it through to production undetected.

Known errors are seeded into the program, and it is up to the automated test suite or QA team to find them.

Rate of detection and remaining undetected bugs are used to measure how the amount of bugs making it through to production.
You will need sufficient amounts of historical data to get an accurate indication of this.

### Conclusion

By using these tools, you may gain insights into the edge cases that exist within your program which would be very hard to catch manually.

I do not consider these tools vital for producing good software but they are definitely helpful, and let's face it, we need all the help we can get.
The results may be thought provoking and lead you to think about your program in different ways.
