# A tale in adopting Alpine Linux for Docker - problems we faced with RSpec testing

If you read Wikipedia you will find that Alpine is a Linux distribution that is based on musl (more on this later) and BusyBox.

With the rise of Docker, it has become a favoured distribution for Docker images due to the greatly reduced size of its images.

At the time of writing, the [Ruby docker images](https://hub.docker.com/_/ruby/tags/) are 343MB in their standard Linux distribution format, but are 28MB in their Alpine flavour.

## The tooling

We use RSpec to test our code, a common testing framework for the Ruby language. 
One of its most distinctive features is the ability to create "hierarchical test suites" by using context blocks.

As an example:

```ruby
describe 'some unit' do
  context 'given something has happened' do
    before { do_something }
    
    context 'when we perform some action' do
      before { some_action }
      
      it 'has happened' do
        expect(result).to have_happened
      end
    end
  end
end
```

These context blocks can get more powerful, and indeed allow sharing of setup between multiple test suites (can be desirable when controlling simulators of external services in tests).

We used Alpine Linux as our Docker image in our Continuous Integration pipeline (CI pipeline), but locally we were using our native Ruby installation at this point in development since there are performance benefits.

What we noticed was our CI pipeline went red:

```
SystemStackError: stack level too deep
  /usr/local/bundle/gems/rspec-support-3.7.0/lib/rspec/support/source/location.rb:10:in `all?'
  /usr/local/bundle/gems/rspec-support-3.7.0/lib/rspec/support/source/location.rb:10:in `location?'
  /usr/local/bundle/gems/rspec-support-3.7.0/lib/rspec/support/source/node.rb:30:in `block in args'
  /usr/local/bundle/gems/rspec-support-3.7.0/lib/rspec/support/source/node.rb:27:in `map'
  /usr/local/bundle/gems/rspec-support-3.7.0/lib/rspec/support/source/node.rb:27:in `args'
  /usr/local/bundle/gems/rspec-support-3.7.0/lib/rspec/support/source/node.rb:45:in `location'
  /usr/local/bundle/gems/rspec-support-3.7.0/lib/rspec/support/source/node.rb:51:in `each'
  /usr/local/bundle/gems/rspec-support-3.7.0/lib/rspec/support/source/node.rb:54:in `block in each'
  /usr/local/bundle/gems/rspec-support-3.7.0/lib/rspec/support/source/node.rb:53:in `each'
  /usr/local/bundle/gems/rspec-support-3.7.0/lib/rspec/support/source/node.rb:53:in `each'
  (...snip many lines...)
  /usr/local/bundle/bin/rspec:29:in `<top (required)>'
```

This was extremely strange since we did not notice this error locally. 

## Step 1: Tracing the error

**What we knew from this error message:**

* The stack size was being restricted within our CI pipeline.

### Increasing the stack size

At first we thought there was an environment configuration difference between the Ruby in our CI pipeline and our local machines.

So we attempted to increase the stack-size within the CI pipeline via the `RUBY_THREAD_VM_STACK_SIZE` environment variable.

This had no effect.

We thought this was very odd, since we still could not reproduce locally.

**What we knew then:**

* The stack size was being restricted within our CI pipeline.
* This was not a configuration issue backed into the Docker image, and changing Ruby configuration did not work (which it should).

### Decreasing the stack size

We then decided to reduce the stack size on our local machines (again with the `RUBY_THREAD_VM_STACK_SIZE` environment variable).

What we discovered was that we needed to have stack sizes <500KB in order to reproduce the issue.

This got us no closer to a fix, but did enable us to see the error locally and trace it to a recursive algorithm within RSpec.

**What we learnt here:**

* The stack size was being restricted within our CI pipeline.
* This was not a configuration issue backed into the Docker image, and changing Ruby configuration did not work (which it should).
* The configuration had an affect locally.

### Running with Alpine locally

Gaining some parity at this point made a lot of sense. While we didn't expect there to be a runtime difference within Ruby between local and Alpine, it was definitely worth ruling it out.

Immediately we noticed the error locally.

```
SystemStackError: stack level too deep
```

**What we took away:**

* The stack size was being restricted within the Alpine docker image
* The `RUBY_THREAD_VM_STACK_SIZE` environment variable had no affect within this docker image

## Step 2: Analyse the problem. What was wrong?

Doing some Google searching we ended up at musl-libc's FAQs, specifically the ["functional differences"](https://wiki.musl-libc.org/functional-differences-from-glibc.html#Thread-stack-size) i.e. incompatibilities with glibc. 

What we learned is that musl provides a default stack size of 80k, which is a significant difference to the stacksize provided by glibc (generally 2MB-10MB).

Moreover, it requires programs to explicitly ask for more (or less) stack via `pthread_attr_setstacksize`, which MRI Ruby does not appear to do.

There is an open Ruby bug here: https://bugs.ruby-lang.org/issues/14387

### What is RSpec doing?

RSpec prints out a list of errors, and helpfully includes a snippet of source code from your test suite.

```
Failures:

  1) 1 equals 2
     Failure/Error: expect(1).to eq(2)

       expected: 2
            got: 1

       (compared using ==)
     # ./spec/test_spec.rb:12:in `block (11 levels) in <top (required)>'

Finished in 0.01589 seconds (files took 0.07908 seconds to load)
1 example, 1 failure

Failed examples:

rspec ./spec/test_spec.rb:11 # 1 equals 2
```

In the example above, the string `expect(1).to eq(2)` is extracted from your test suite source code.

The way it does is that it parses your Ruby source code using [Ruby ripper](http://ruby-doc.org/stdlib-2.5.0/libdoc/ripper/rdoc/Ripper.html), and then searches for the relevant nodes in the Ruby language Abstract Syntax Tree (AST). The more deeply nested our context blocks were in our RSpec specs, the more recursion occurred during this process.

This requires a Depth-First-Search algorithm, which is more elegant when expressed as a recursive algorithm.

## Step 3: How we solved the error

We submitted a [patch upstream to RSpec](https://github.com/rspec/rspec-support/pull/343) to change the implementation from a recursive algorithm to a loop-based algorithm that does not use the stack.

Ultimately this is a temporary fix, as any recursive logic could be a source of errors in production. This should be solved at the Ruby language level.

## The whiff of a larger design smell

This is a Liskov-substitution principle violation.

*Liskov substituion principle?? That's an object-oriented principle? How does a stack overflow error caused by libc relate to Objects?*

The dependency of what libc implementation is used is controlled by the Linux distribution (the caller of your Ruby application). This means the dependency is inverted, and we are looking at an object-oriented design.

If you consider `musl-libc` and `glibc` as implementing an interface called `libc`, then you will notice that they must also be Liskov-compatible to ensure smooth operation.

The imperfection here is that their public APIs are slightly different, which in Alpine's case is by choice. 
Alpine linux is derived from the [LEAF Project](https://en.wikipedia.org/wiki/LEAF_Project), which specifically targets low-powered hardware. The sort of hardware that would not have much space for 2MB-10MB of memory allocated for a stack.

The interesting implication here is the community has decided to use, by defacto choice, a Linux distribution that has historically made some design choices to achieve both low memory and disk-size footprint. In our modern cloud environments, where we can spare 2-10MB of memory allocation for a stack, these design choices don't appear to apply.

The impact is that the Ruby codebase must be aware of what version of libc it is running against in order to provide a stable programming language to us Ruby developers.
This is undesirable to the Ruby language developers, as it creates a reverse dependency on musl-libc, which increases the total cost of maintaining Ruby (if musl changes, so must Ruby). 

Ideally, the community that maintain libc implementations need to work together to expose the same behaviour (and agree on what this behaviour looks like). 

In reality, it is very difficult to achieve this. In practical terms, musl-libc has proven to be a very good replacement for glibc, and certainly provides a desirable disk-size footprint.

As software engineers, choosing Alpine over a fatter base image requires consideration of the functional differences that musl-libc has compared to glibc. It is very likely that you will encounter issues, and when you do it is time saving to know where to look first.
