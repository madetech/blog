The Anatomy Of The Perfect Object
----------------------------------
  - Functional core imperative shell
  - Referential transparency
  - 1 public method
  - Principle of least surprise
  - Small methods

Disclaimer
-----------
  I am a Ruby programmer and this blog post will focus mainly on Ruby.

The perfect object is two objects
----------------------------------
  Functional programmers place high value and trust in systems that are referentially transparent.
  That is systems that accept input as explicit arguments, operate on the input and return output.
  These are considered dependable because they are not affected by the outside world beyond what they are given as arguments.

  Since we operate in an object oriented environment, it is not that easy (impossible) for us to achieve such designs.
  The best we can do is to group stateful actions as closely together as possible.
  These stateful objects then reach down into referentially transparent objects.

1 Public Method
----------------
  In the functional core your objects should have only 1 public method, with private methods to assist it in achieving it's goals.

The Principle of Least Surprise
--------------------------------
  Don't try and be fancy.  Write the most boring code possible.  Write it as if a 5 year old was going to inherit the code base from you.
  Long descriptive names are always better than short ones or abbreviations.
