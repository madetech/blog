# TDD, unit testing and rspec

Before joining Made, my experience with unit testing was always with PHPUnit. It's very flexible in allowing you to write tests quickly; create a class, add some methods that start with `test`, include some exceptions, and away you go. What I don't think it allows you to do well is think about how to structure your tests, and what to focus them on. For that you have to rely on experience and good discipline.

***

There are many ways to structure rspec tests. It doesn't restrict you to write them in one single way. It just tries to guide you in an opinionated direction. Whether you agree with that direction is up to you.

```
describe Warehouse do
  context 'when turning warehouse power off, all machines are powered off' do
    warehouse = Warehouse.new(power: true)
    machine = Machine.new(name: 'Vending machine', power_switch: true)

    warehouse.machines << machine

    expect(machine.power).to be_true

    warehouse.power_off

    expect(warehouse.power).to be_false
    expect(machine.power).to be_false
  end
end
```

The above is quite a common way of writing tests regardless of what language or test framework you're using. But there is a lot happening in that one test:

 * Description of what to test
 * Creation of objects that we'll be using in our tests
 * Setup the state of the objects
 * Assertions

It's a bit mashed together. What are we actually testing? What if we want to reuse objects between tests?

We actually have two subjects that we're testing here. The first is the Warehouse building, and that if we use a convienience method `power_off`, we want to ensure there's no power.

Also, we want to test the Machines in the warehouse. If the machine's power switch is on, it's power state will be affected by the Warehouse.

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

And the machines:

(Explain briefly about factory girl, and defaults, and default associations)

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

Explain how we've structured the various parts of the test

 * `let` for object creation
 * `context` to break down the test into smaller pieces
 * `before` to setup object states
 * `subject` to be clear on what we're testing (also, as a hint, if you start testing other objects, should possibly be in separate unit test for that class
 * `it` and `its` assertions
