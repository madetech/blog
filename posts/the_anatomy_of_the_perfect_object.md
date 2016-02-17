The Service Object / Value Object pair in Ruby
-----------------------------------------------

  - State as a separation of concerns
  - The anatomy of the single public method
  - Hashes as the transport mechanism
  - The poor mans referential transparency
  - Principle of least surprise
  - Small methods
  - Easy testing

Introduction
-------------
  When solving requirements for a system, you should extract specific roles out into service objects.
  These are known as PORO's in Ruby and you want a lot of them.

  The lazy path is to solve problems directly where you encounter them such as the controller, model or view (If you are using MVC).

  You are missing a 'code seam' where you can hook into to get the desired functionality from.

  Instead you should create very simple, small objects (generally less than a hundred lines), with verbose names describing exactly what problem
  they solve.

State as a separation of concerns
---------------------------------
  Functional programmers place high value and trust in systems that are referentially transparent.
  That is systems that accept input as explicit arguments, operate on the input and return output.
  These are considered dependable because they are not affected by the outside world beyond what they are given as arguments.

  A referentially transparent (or pure) function will always return the same output given the same input.

  In this setup I propose having two objects.  One which does state and another one which operates only on it's arguments.
  The non-stateful object is also known as a value object.  It exists to represent the data needed by the stateful object exactly.
  In a perfect world your data would be perfect and conform to the exact requirements of your program but this is hardly ever the case.

  The stateful objects do things like write to databases, set sessions, upload csv's and all those other volatile things which are undependable might fail.
  The non-stateful objects on the other hand are more predictable.
  They are easy to test and require no interaction with the outside world.

The anatomy of the single public method
----------------------------------------
  Apart from the constructor, there should be only one public method that you can call.
  This method is special and should be comprised of only methods that you have defined.
  It should be a sequence of steps and by simply reading it you should be able to understand everything the object does.
  Notice that below every method sits at the same level of abstraction.  A layer of abstraction that we have defined.

  Good

    def register_employee
      find_or_create_user
      set_user_as_employee

      notify_via_email
    end

  Bad

    def register_employee
      find_or_create_user
      set_user_as_employee

      mail('foo@example.com', 'Welcome new employee')
    end

  The mail method above is an abstraction that sits at a lower level than the rest of the methods.
  This applies to both the value objects that are instantiated in the service object and the service object itself.
  In fact all methods that you write should adhere to this principle.

Hashes as the transport mechanism
----------------------------------
  Hashes are beatiful data-structures that are comprised of keys and values.
  They are descriptive enough to make sense on their own just by reading the contents.

  I instantiate both the service objects and value objects with hashes.

  By doing this you do not have to consider the order of arguments when being passed to a method.

  Always prefer to use the .fetch method over [ for accessing values that you expect to be present.
  This is important because it will throw a key not found error instead of having a nil value percolate through your stack undetected.

The Principle of Least Surprise
--------------------------------
  Never try be fancy with code.

  Write the most boring code possible.  Write it as if a 5 year old was going to inherit the code base from you.
  Long descriptive names and no abbreviations are the law.

  If something could be given a name, do it.  first_name is much more intention revealing than person[0].

Easy testing
-------------
  When testing these objects, you only assert the outcome of the one public method that the object has.

  With the service object / value object pair testing becomes much easier.
  For testing the value object it need simply be instantiated with a (hash / map) of params and you can assert that it has transformed the data into
  the values you require (a hash / map).

  Testing the service object itself has also become easier as the only thing you need to test is how it affects the world.

Disclaimer
-----------
  I am a Ruby programmer and this blog post will focus mainly on Ruby.
  These principles should apply to whichever language you use but it is mainly imperative languages where we have to be extra disciplined.
