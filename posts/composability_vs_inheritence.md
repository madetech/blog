# Composition versus Inheritence

Before I compare composition and inheritence I'll start with my definitions
of both of them.

Composition is the splitting of complex business rules into simpler pieces.
These pieces are unaware of one another and are generally useless alone. When
these simple composable units are put together, or composed, they perform
business requirements.

``` ruby
class BankAccount < Struct.new(:amount)
end

class Withdrawer
  def withdraw(account, amount)
    account.amount -= amount
  end
end

class Depositor
  def deposit(account, amount)
    account.amount += amount
  end
end

class Transferrer
  def transfer(from_account, to_account, amount)
    Withdrawer.new.withdraw(from_account, amount)
    Depositor.new.deposit(to_account, amount)
  end
end

fred = BankAccount.new(100)
luke = BankAccount.new(0)
Transferrer.new.transfer(fred, luke, 100)
```

Inheritence is the sharing of business logic by class hierarchy. This hierarchy
is declared by one unit of logic stating it extends another. In most Object
Oriented languages a class will extend another inheriting it's parents methods.

``` ruby
module Depositable
  def deposit(amount)
    amount += amount
  end
end

module Withdrawable
  def withdraw(amount)
    amount -= amount
  end
end

module Transferable
  def transfer(to_account, amount)
    withdraw(amount)
    to_account.deposit(amount)
  end
end

class BankAccount < Struct.new(:amount)
  include Depositable
  include Withdrawable
  include Transferable
end

fred = BankAccount.new(100)
luke = BankAccount.new(0)
fred.transfer(luke, 100)
```
