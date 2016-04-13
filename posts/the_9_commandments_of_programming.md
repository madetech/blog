# The 9 commandments of programming

 1. Never use variables
 2. Never use if/switch/ternary statements
 3. Never use inheritance
 4. Never use setters
 5. Never use instance variables
 6. Never have more than one line per method body
 7. Never have more than one public method per class
 8. Never mutate any object
 9. Break any of the previous rules within encapsulated interfaces

## 1. Never use variables

Variables can change, this fact is indicated by their name. The more parts of
your program that can change, the harder your program will be to reason with.
It is for this reason you should try to avoid using them.

``` ruby
def handle_request(request)
  response = {}

  if request.erroneous?
    response[:status] = 500
  else
    response[:status] = 200
  end
  
  response[:body] = build_response_body(request)
  response
end
```

``` ruby
def handle_request(request)
  if request.erroneous?
    erroneous_response(request)
  else
    success_response(request)
  end
end

def erroneous_response(request)
  { status: 500, body: build_response_body(request) }
end

def success_response(request)
  { status: 200, body: build_response_body(request) }
end
```

## 2. Never use if/switch/ternary statements

Conditional statements such as if, switch and ternary add pathways to your
program. The more pathways the harder your program will be to reason with.
Do you see where I'm going with all this?

``` ruby
class Sku::Exporter
  def export(sku, format = :txt)
    case format
    when :csv
      Sku::CsvFormatter.new.format(sku.attributes)
    when :json
      sku.attributes.to_json
    end
  end
end
```

``` ruby
class Sku::Exporter < Struct.new(:formatter)
  def export(sku)
    formatter.new.format(sku.attributes)
  end
end

Sku::Exporter.new(Sku::CsvFormatter.new).export(sku)
```

The thing with conditionals is that you do actually require them to build
programs that perform a variety of functions. Maybe if your program did
one thing then perhaps you wouldn't require. However most do.

## 3. Never use inheritance
