# Focus with well structured rspec tests

Before joining Made, my experience with unit testing was always with PHPUnit. It's very flexible in allowing you to write tests quickly; create a class, add some methods that start with `test`, include some assertions, and away you go. What I don't think PHPUnit—and similar—allow you to do well is think about how to structure your tests, and what to focus them on. For that you have to rely on experience and good discipline.

Take the following example test in rspec, written in 'retro' style:

```
describe Warehouse do
  context 'when turning warehouse power off' do
    it 'should turn all machines off' do
      warehouse = Warehouse.new(power: true)
      machine = Machine.new(name: 'Vending machine', power_switch: true)

      warehouse.machines << machine

      expect(machine.power).to be_true

      warehouse.power_off

      expect(warehouse.power).to be_false
      expect(machine.power).to be_false
    end
  end
end
```

The above example is quite a common way of writing tests regardless of what language or test framework you're using. But there is a lot happening in that one test:

 * Description of what to test
 * Creation of objects that we'll be using in our tests
 * Setup the state of the objects
 * Assertions

It's a bit mashed together. What are we actually testing? What if we want to reuse objects between tests?

We actually have two subjects that we're testing here. The `Warehouse` and the `Machine` objects within it. At this level of testing, these should really be broken out into their own test specs:

```
describe Warehouse::Building do
  let(:warehouse) { create(:warehouse_building, power: true) }

  subject { warehouse }

  context 'when switching off power' do
    before(:each) do
      warehouse.power_off
    end

    its(:power) { is_expected.to be_false }
  end

  context 'when switching power on' do
    before(:each) do
      warehouse.power_on
    end

    its(:power) { is_expected.to be_true }
  end
end
```

And the corresponding `Machine` test:

```
describe Warehouse::Machine do
  let(:machine) { create(:warehouse_machine) }

  subject { machine }

  context 'when switched on, and turning warehouse power off' do
  	 before(:each) do
  	   machine.warehouse.power_off
  	 end

  	 its(:power) { is_expected.to be_false }
  end

  context 'when switched off, and turning warehouse power on' do
    before(:each) do
      machine.power_switch = false
      machine.warehouse.power_on
    end

    its(:power) { is_expected.to be_false }
  end
end
```

Don't read too much into what's going on with the code example, the thing to take away is the structure of the test, and it's readability.

## Breaking down the structure

The test structure mirrors the _Given-When-Then_ pattern, derived from Behaviour Driven Development.

 * Given: Setup your tests using `let` and `before` blocks
 * When: Define your test `subject`
 * Then: Use `it` and/or `its` to make your assertions

### Setting the scene

Using `let` along with Factory Girl to setup our test subjects allows us to have sensible defaults in a separate factory file so that our tests remain cleaner. Having these stored in a `let` block allows for reuse between tests, where the value is cached after it's first use, but not between our test assertions.

That means that we can use our `let` values when setting up our tests. And we do that using `before` blocks.

Why use a `before` block rather than just doing setup in a `subject` block? Simply because it reads better.

Rather than:

```
subject do
  setup_this
  and_that
  test_this
end
```

Do this:

```
before(:each) do
  setup_this
  and_that
end

subject { test_this }
```

### Great Expectations

Once the tests are all setup and ready, it's time for those assertions. Depending on your test subject, you might choose to use `it` or `its`. 

When testing objects, it's always good to use `its` as you can easily test multiple properties and methods by simply passing the name as the first argument.

```
its(:power) { is_expected.to be_false }
```

The above is basically doing this behind the scenes:

```
expect(subject.power).to be_false
```

If you have multiple assertions to make, then you'd have a lot of lines repeated that look similar, so `its` is a much clearer way of defining them.

For other data types, `it` might be a better fit. An array for example:

```
it { is_expected.to include('Apple') }
```

Try and keep the assertions as simple and as minimal as possible. If you find yourself writing a lot of assertions in a single context, perhaps try breaking them out into a separate context.

***

With the various rspec helpers on offer, you're able to be more disciplined in writing well structured tests, that read better, while remaining focused on small pieces of functionallity. Consider the readability at all times, as your tests often turn out to be great documentation for others.
