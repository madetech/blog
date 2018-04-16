# An Alpine linux gotcha and what it means for you

If you read Wikipedia you will find that Alpine is a linux distribution that is based on musl (more on this later) and BusyBox.

With the rise of Docker, it has become a favoured distribution for Docker images due to the favourably small size of it's images.

At the time of writing, the [Ruby docker images](https://hub.docker.com/_/ruby/tags/) are 343MB in their standard linux distribution format, but are 28MB in their Alpine flavour.

## The tooling

We use RSpec to test our code, a common testing framework for the Ruby language. 
One of it's most powerful features is the ability to create "hierarchical test suites" by using context blocks

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

We used Alpine linux as our docker image in our CI-pipeline, but locally we were using our native Ruby installation at this point in development since there are performance benefits.

What we noticed was our CI-pipeline went red:

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
  /usr/local/bundle/gems/rspec-core-3.7.1/lib/rspec/core/formatters/snippet_extractor.rb:118:in `location_nodes_at_beginning_line'
  /usr/local/bundle/gems/rspec-core-3.7.1/lib/rspec/core/formatters/snippet_extractor.rb:96:in `expression_node'
  /usr/local/bundle/gems/rspec-core-3.7.1/lib/rspec/core/formatters/snippet_extractor.rb:88:in `line_range_of_location_nodes_in_expression'
  /usr/local/bundle/gems/rspec-core-3.7.1/lib/rspec/core/formatters/snippet_extractor.rb:57:in `line_range_of_expression'
  /usr/local/bundle/gems/rspec-core-3.7.1/lib/rspec/core/formatters/snippet_extractor.rb:42:in `expression_lines'
  /usr/local/bundle/gems/rspec-core-3.7.1/lib/rspec/core/formatters/snippet_extractor.rb:31:in `extract_expression_lines_at'
  /usr/local/bundle/gems/rspec-core-3.7.1/lib/rspec/core/formatters/exception_presenter.rb:218:in `read_failed_lines'
  /usr/local/bundle/gems/rspec-core-3.7.1/lib/rspec/core/formatters/exception_presenter.rb:163:in `failure_slash_error_lines'
  /usr/local/bundle/gems/rspec-core-3.7.1/lib/rspec/core/formatters/exception_presenter.rb:150:in `block in failure_lines'
  /usr/local/bundle/gems/rspec-core-3.7.1/lib/rspec/core/formatters/exception_presenter.rb:149:in `tap'
  /usr/local/bundle/gems/rspec-core-3.7.1/lib/rspec/core/formatters/exception_presenter.rb:149:in `failure_lines'
  /usr/local/bundle/gems/rspec-core-3.7.1/lib/rspec/core/formatters/exception_presenter.rb:34:in `colorized_message_lines'
  /usr/local/bundle/gems/rspec-core-3.7.1/lib/rspec/core/formatters/exception_presenter.rb:240:in `formatted_message_and_backtrace'
  /usr/local/bundle/gems/rspec-core-3.7.1/lib/rspec/core/formatters/exception_presenter.rb:86:in `fully_formatted_lines'
  /usr/local/bundle/gems/rspec-core-3.7.1/lib/rspec/core/formatters/exception_presenter.rb:78:in `fully_formatted'
  /usr/local/bundle/gems/rspec-core-3.7.1/lib/rspec/core/notifications.rb:200:in `fully_formatted'
  /usr/local/bundle/gems/rspec-core-3.7.1/lib/rspec/core/notifications.rb:114:in `block in fully_formatted_failed_examples'
  /usr/local/bundle/gems/rspec-core-3.7.1/lib/rspec/core/notifications.rb:113:in `each'
  /usr/local/bundle/gems/rspec-core-3.7.1/lib/rspec/core/notifications.rb:113:in `each_with_index'
  /usr/local/bundle/gems/rspec-core-3.7.1/lib/rspec/core/notifications.rb:113:in `fully_formatted_failed_examples'
  /usr/local/bundle/gems/rspec-core-3.7.1/lib/rspec/core/formatters/base_text_formatter.rb:32:in `dump_failures'
  /usr/local/bundle/gems/rspec-core-3.7.1/lib/rspec/core/reporter.rb:206:in `block in notify'
  /usr/local/bundle/gems/rspec-core-3.7.1/lib/rspec/core/reporter.rb:205:in `each'
  /usr/local/bundle/gems/rspec-core-3.7.1/lib/rspec/core/reporter.rb:205:in `notify'
  /usr/local/bundle/gems/rspec-core-3.7.1/lib/rspec/core/reporter.rb:175:in `block in finish'
  /usr/local/bundle/gems/rspec-core-3.7.1/lib/rspec/core/reporter.rb:191:in `close_after'
  /usr/local/bundle/gems/rspec-core-3.7.1/lib/rspec/core/reporter.rb:171:in `finish'
  /usr/local/bundle/gems/rspec-core-3.7.1/lib/rspec/core/reporter.rb:81:in `report'
  /usr/local/bundle/gems/rspec-core-3.7.1/lib/rspec/core/runner.rb:112:in `run_specs'
  /usr/local/bundle/gems/rspec-core-3.7.1/lib/rspec/core/runner.rb:87:in `run'
  /usr/local/bundle/gems/rspec-core-3.7.1/lib/rspec/core/runner.rb:71:in `run'
  /usr/local/bundle/gems/rspec-core-3.7.1/lib/rspec/core/runner.rb:45:in `invoke'
  /usr/local/bundle/gems/rspec-core-3.7.1/exe/rspec:4:in `<top (required)>'
  /usr/local/bundle/bin/rspec:29:in `load'
  /usr/local/bundle/bin/rspec:29:in `<top (required)>'
```

This was extremely strange since we did not notice this error locally. 

## Tracing the error

### Increasing the stack size

At first we thought there was an environment configuration difference between the Ruby in our CI pipeline and our local machines.

So we attempted to increase the stack-size with the CI environment via the `RUBY_THREAD_VM_STACK_SIZE` environment variable.

This had no effect.

We thought this was very odd, since we still could not reproduce locally.

### Decreasing the stack size

We then decided to attempt to reduce the stack size on our local machines (again with the `RUBY_THREAD_VM_STACK_SIZE` environment variable).

What we discovered was that we needed to have stack sizes <500KB in order to reproduce the issue.

This got us no closer to a fix, but did tell us that somehow the stack size was being restricted in our CI environment.

### Running with Alpine locally

Gaining some parity at this point made a lot of sense. While we didn't expect there to be a runtime difference within Ruby between local and Alpine, it was definitely worth ruling it out.

Immediately we noticed the error locally.

```
SystemStackError: stack level too deep
```

## What was wrong?

Doing some google searching we ended up at musl-libc's FAQs, specifically the ["functional differences"](https://wiki.musl-libc.org/functional-differences-from-glibc.html#Thread-stack-size) i.e. incompatibilities between glibc. 

What we learned is that musl provides a default stack size of 80k, which is a significant difference to the stacksize provided by glibc (generally 2MB-10MB).

Moreover, it requires programs to explicitly ask for more (or less) stack via `pthread_attr_setstacksize`, which MRI Ruby does not appear to do.

There is an open Ruby bug here: https://bugs.ruby-lang.org/issues/14387

## How did we solve it?

We submitted a [patch upstream to RSpec](https://github.com/rspec/rspec-support/pull/343) to change the implementation from a recursive algorithm to a loop-based algorithm that does not use the stack.

Ultimately this is a temporary fix, as any recursive logic could be a source of errors in production. This should be solved at the Ruby language level.

## Design problems

This is a liskov substition principle violation.

*Object-orientism? How does that come in?*

The dependency on what libc implementation is used is controlled by the Linux distribution (the caller of your Ruby application).

If you consider musl-libc and glibc as implementing the "libc" interface, then you will notice that they must also be liskov compatible.

The imperfection is that their public APIs are slightly different, possibily by mistake, or probably by choice.

The impact is that the Ruby codebase must be aware of what version of libc it is running against in order to provide a liskov-compliant programming language.

This is undesirable, as it creates a reverse dependency on musl-libc, which increases the total cost of maintaining Ruby (if musl changes, so must Ruby). 





