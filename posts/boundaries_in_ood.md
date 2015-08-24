# Data and Behaviour;<br />Inheritance and Functional Composition

As responsible programmers we like to write programs to the best of our ability.
As our profession has evolved so too have our languages and the tools we use.
We identify around concepts, patterns and principles.

Today I want to explore 4 common programming concepts together. I want to
illustrate how they relate to each other and finally I want to draw
conclusions on how they can work together to build better programs.

Of course from the title of this post you already know what four concepts I
am talking about. Data, behaviour, inheritance and functional composition.
However from the title I have also paired them, data and behaviour,
inheritance and functional composition. This pairing is intentional as you will
discover shortly.

## Data and Behaviour

Object oriented languages, such as Ruby, focus on structuring programs as
objects. These languages bring together data and behaviour or rather fields and
methods into one unit, the object.

A traditional way to structure the idea of a bank account in an OOP language
would be to use a single object `BankAccount`. Before going straight into this
example, let's first think about a bank account. It has a balance which is a
number that represents how much money is held within the account. You can also
perform actions or behaviours on the bank account, such as withdrawing and
depositing money from and to it. In an object, the balance would be data, and
the actions of withdrawing and depositing would be methods.

In ruby, a bank account might look something like this:

``` ruby
class BankAccount
  attr_reader :balance

  def initialize(balance)
    @balance = balance
  end

  def withdraw(amount)
    @balance -= amount
  end

  def deposit(amount)
    @balance += amount
  end
end
```

In this example we have the `@balance` field and three methods `#initialize`,
`#withdraw` and `#deposit`. The balance is a number that can be increased or
decreased by withdrawing or depositing an amount into the bank account.

Let's use the example above to do some withdrawing and depositing.

``` ruby
lukes_account = BankAccount.new(100)
lukes_account.withdraw(10)
lukes_account.deposit(30)
puts lukes_account.balance # => 120
```

In this usage example we assign an instance of the `BankAccount` class to a
variable `lukes_account` and then perform actions upon the account.

You can see why object oriented languages are so attractive. The ability to
think of real world objects as objects in your programming language is useful
for haivng a mental model of your program. Languages like smalltalk took this
a lot further, providing an IDE for the language which literally draw the
objects and their relationships with each other on the programmers screen.

So data and behaviour: both useful concepts traditionally encapsulated together
in one object.

## Inheritance

Inheritance is another common object oriented concept. By using hierarchy
behvaiour can be shared and adapted. This hierarchy is declared by one class
extending another.

Coming back to the bank account example, you might use inheritance to convey
the relationship between a child's bank account and a standard one. The child's
account may have a lower limit on the amount of money that may be taken out at
one time.

First of all let's apply a limit to the standard account:

``` ruby
class BankAccount
  class AmountExceedsWithdrawLimitError < RuntimeError; end

  attr_reader :balance, :limit

  def initialize(balance)
    @balance = balance
    @limit = 200
  end

  def withdraw(amount)
    if amount > limit
      raise AmountExceedsWithdrawLimitError
    else
      @balance -= amount
    end
  end

  def deposit(amount)
    @balance += amount
  end
end
```

And now let's extend our bank account to represent a child account with
a lower limit:

``` ruby
class ChildBankAccount < BankAccount
  def initialize(*)
    super
    @limit = 50
  end
end
```

Here our `ChildBankAccount` extends `BankAccount` and overrides the
`#initialize` method to change the account limit after calling the original
implementation of `#initialize` with `#super`.

Immediately you see the continued attractiveness of object oriented languages.
You can represent classes of things and their hierarchy. Descendants share
properties with their ancestors but can also diverge from their data and
behaviours.

## Functional composition

Functional composition is often a foreign concept to object oriented programmers
and rightly so as it's a functional language concept.

Function composition breaks away from the idea of keeping behaviour in one
real world object. In fact in functional languages, behaviour is contained
within functions only. The composition of these functions then build up the
behaviour of the program. Going back to our bank account example, instead of
having the behaviour within the bank account object you would instead have
other objects representing the actions that can be taken on a bank account.

In our ruby example we might reduce our bank account object to have just it's
initialize and balance accessor:

``` ruby
class BankAccount
  attr_reader :balance, :limit

  def initialize(balance)
    @balance = balance
    @limit = 200
  end
end
```

The `BankAccount` becomes a container for data only. No longer is the bank
account in charge of withdrawing and depositing. It's role now is to hold the
balance and withdraw limit of the account.

We should also create our child bank account whilst we're at it:

``` ruby
class ChildBankAccount < BankAccount
  def initialize(*)
    super
    @limit = 50
  end
end
```

Nothing new here but it's worth noting this `ChildBankAccount` is behaviourless
and just a container for data like `BankAccount`.

So we have our data described, what about our behaviour? To represent the
withdraw and deposit behaviour we need two new composable objects:

``` ruby
class Withdrawer
  class AmountExceedsLimitError < RuntimeError; end

  def withdraw(account, amount)
    if amount > account.limit
      raise AmountExceedsLimitError
    else
      account.balance -= amount
    end
  end
end

class Depositor
  def deposit(account, amount)
    account.balance += amount
  end
end
```

Both `Withdrawer` and `Depositor` do not store any data and instead only act on
data given to them as arguments. Lonesome, standalone behaviour. Your eyebrows
may well be raising but let me run the examples course a little longer.

In order to enact on the `BankAccount` object we would have to use the
objects in concert:

``` ruby
lukes_account = BankAccount.new(100)
Withdrawer.new.withdraw(lukes_account, 10)
Depositor.new.deposit(lukes_account, 30)
puts lukes_account.balance # => 120
```

Now we are functionally equivalent to our pure inheritance example. The example
admitedly involves more objects than before.

To fully explore functional composition, we need to actually compose something.
One real life example would be the act of transferring money from one account to
another. The act of transferring money involves withdrawing from one account
and depositing in another.

Representing the transferral of money in ruby with functional composition
would probably look something like this:

``` ruby
class Transferrer
  def transfer(from_account, to_account, amount)
    Withdrawer.new.withdraw(from_account, amount)
    Depositor.new.deposit(to_account, amount)
  end
end
```

We have now composed two functions into a third function. That third function
is now more complex than the other two but looks simple since it delegates out
to well named pieces of functionality.

Now we can use the `Transferrer` object to move money from my account to a
friends:

``` ruby
lukes_account = BankAccount.new(100)
freds_account = BankAccount.new(0)
Transferrer.new.transfer(lukes_account, freds_account, 20)
puts lukes_account.balance # => 80
puts freds_account.balance # => 20
```

The `Transferrer` object sums up the power of functional composition. It isn't
a crushendo of a summary, but you have to take a step back a think about it.

We have composed two units of work into a third larger concept. This kind of
composition gives us the ability to write small units of work and compose
them together into bigger ideas. We can continue to stack concepts on top of
one another to create an entire application.

## Unifying the two worlds

Unless you're a functional flirter or fanatic you may not yet see the advantages
of using composable functions over wrapping larger concepts in objects.

If you're a rails programmer you will have seen some rather large objects in
your time. You'll know that classes become harder and harder to reason about
the more lines they have. Ask yourself for a moment:

> Why are objects with many methods harder to reason about?

The answer to this question lies in the boundaries or lack thereof in large
objects. Remember, objects are encapsulations of ideas. The greater that idea
gets the harder it will eventually be to grasp. The more data an object is
responsibile for, the more behaviour it has, the harder it is to fit into your
brain.

Functional composition is a remedy for when things get too tough. I wouldn't
argue you should build your rails apps with everything split out into tiny
units of work. I would argue that when things get tough functional composition
can make things easier for you.

The more data an object has, the more moving parts, the harder it is to get
under test. If it's hard to get under test, it's probably hard for your head
to think about too. It's a sign that you've pushed your object too far.

Let's go back to our example one more time. I want to implement the transfer
functionality without composition:

``` ruby
class BankAccount
  class AmountExceedsWithdrawLimitError < RuntimeError; end

  attr_reader :balance, :limit

  def initialize(balance)
    @balance = balance
    @limit = 200
  end

  def withdraw(amount)
    if amount > limit
      raise AmountExceedsWithdrawLimitError
    else
      @balance -= amount
    end
  end

  def deposit(amount)
    @balance += amount
  end

  def transfer(to_account, amount)
    withdraw(amount)
    to_account.deposit(amount)
  end
end
```

As our object gets larger, and let's be honest this object isn't that large yet,
it will have an increasing amount of responsibilities. The more responsibilities
the more edge cases that object may have. The more complicated your tests will
be to setup and tear down.

Let's use our remedy to keep the same interface above, but move our logic out
into composable units that can be individually tested away from the
`BankAccount`:

``` ruby
class BankAccount
  attr_reader :balance, :limit

  def initialize(balance)
    @balance = balance
    @limit = 200
  end

  def withdraw(amount)
    Withdrawer.new.withdraw(self, amount)
  end

  def deposit(amount)
    Depositor.new.deposit(self, amount)
  end

  def transfer(to_account, amount)
    Transferrer.new.transfer(self, to_account, amount)
  end
end
```

We have fused our two ideas together. Now we have one object, a `BankAccount`
that still encapsulates all the behaviours associated with a bank account.
However we've drawn some boundaries. We now have other objects responsible for
carrying out the behaviour. These composable units only accept data via their
method parameters, no other complexity can travel through into them.

Lines are important for our mental well being as programmers. Knowing when and
where to draw a line can help you reason about your program that much easier.

When you draw a line with an interface you now have two separate concerns that
are individually testable. Not only that but your mental model only has to
concern itself up to the line. This allows you to mentally step through your
program a lot better than if everything were in one file.

Without these lines both you and your program are essentially evaluating in a
global scope. We all know how bad globals are, don't we?
