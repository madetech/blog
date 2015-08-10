# Composability versus Inheritence

As responsible programmers we like to keep our programs DRY, that is, we do not
like to repeat ourselves. Object Oriented languages provide us a number of
useful ways to share logic within a system to keep things DRY.

Composability and Inheritence are two such ways of not repeating yourself. They
both have their uses but I suspect more people lean on the latter rather than
the former. In this post I'll describe them both and then provide a comparison.

## Composability

Composability refers to the practice of splitting complex business rules into
simpler pieces. I'll refer to these pieces as composable functions.
These pieces are unaware of one another and are generally useless alone. When
these simple composable units are put together, or composed, they perform
business requirements.

``` ruby
class BankAccount < Struct.new(:balance)
end
```

Our first piece of the puzzle is our BankAccount object. It is a struct that
has one field, `#balance`. This class' role is to store the `BankAccount`'s
balance.

``` ruby
class Withdrawer
  def withdraw(account, amount)
    account.balance -= amount
  end
end

class Depositor
  def deposit(account, amount)
    account.balance += amount
  end
end
```

The next two pieces are the `Withdrawer` and `Depositor`. They know how to
withdraw and deposit, from and to, respectively. What this means in logic terms
is they know how to deduct and increase the `BankAccount#balance`. Both classes
are useful in their own right.

``` ruby
class Transferrer
  def transfer(from_account, to_account, amount)
    Withdrawer.new.withdraw(from_account, amount)
    Depositor.new.deposit(to_account, amount)
  end
end
```

The last piece is `Transferrer` which composes `Withdrawer` and `Depositor`
together to perform another useful task, that of transferring money from one
account to another.

``` ruby
fred = BankAccount.new(100)
luke = BankAccount.new(0)
Transferrer.new.transfer(fred, luke, 100)
```

To finish it all off, a use case of `Transferrer`.

## Inheritence

Inheritence is the sharing of business logic by class hierarchy. This hierarchy
is declared by one unit of logic stating it extends another. In most Object
Oriented languages a class will extend another inheriting it's parents methods.
In ruby you can also include modules in your classes, this itself is a form
of inheritence since it adds the module to the classes ancestors array.

``` ruby
module Depositable
  def deposit(amount)
    balance += amount
  end
end

module Withdrawable
  def withdraw(amount)
    balance -= amount
  end
end
```

This time we start with our modules, `Depositable` and `Withdrawable`. They
perform individual roles just like their composable counterparts
`Depositor` and `Withdrawer`.

``` ruby
module Transferable
  def transfer(to_account, amount)
    withdraw(amount)
    to_account.deposit(amount)
  end
end
```

A third module, `Transferable` provides similar functionality to `Transferrer`
but calls `#withdraw` on itself and `#deposit` on the injected bank account.
This is because `Transferable` gives it's role to another class when included.

``` ruby
class BankAccount < Struct.new(:balance)
  include Depositable
  include Withdrawable
  include Transferable
end
```

Here is the inherited version of `BankAccount`. It includes all three modules
defined and therefore takes on each of their roles. We now have an object
that embodies all the behaviours at once.

``` ruby
fred = BankAccount.new(100)
luke = BankAccount.new(0)
fred.transfer(luke, 100)
```

Finally again, a use case of `BankAccount#transfer`. As you can see the
`BankAccount` objects can deal with each other without any third parties.
