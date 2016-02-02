The Anatomy Of The Perfect Object
----------------------------------
  - State as a separation of concerns
  - Referential transparency
  - 1 public method is in good taste
  - Principle of least surprise
  - Small methods

Disclaimer
-----------
  I am a Ruby programmer and this blog post will focus mainly on Ruby.
  These principles should apply to whichever language you use but it is mainly imperative languages where we have to be extra disciplined.

The perfect object is two objects
----------------------------------
  Functional programmers place high value and trust in systems that are referentially transparent.
  That is systems that accept input as explicit arguments, operate on the input and return output.
  These are considered dependable because they are not affected by the outside world beyond what they are given as arguments.

  In this setup I propose having two objects.  One which does state and another one which operates only on it's arguments.
  The non-stateful object is also known as a value object.  It exists to represent the data needed by the stateful object exactly.
  In a perfect world your data would be perfect and conform to the exact requirements of your program but this is hardly ever the case.

  The stateful objects do things like write to databases, set sessions, upload csv's and all those other volatile things which might fail.
  The non-stateful objects on the other hand are more predictable.  They are easy to test and require no interaction with the outside world.

1 Public Method as a matter of good taste.
-------------------------------------------
  In the functional core your objects should have only 1 public method, with private methods to assist it in achieving it's goals.

The Principle of Least Surprise
--------------------------------
  Don't try and be fancy.  Write the most boring code possible.  Write it as if a 5 year old was going to inherit the code base from you.
  Long descriptive names are always better than short ones or abbreviations.
