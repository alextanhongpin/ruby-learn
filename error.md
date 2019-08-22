# Raising errors

```ruby
class Person
  def initialize(name)
    raise ArgumentError, "No name present" if name.empty?
    @name = name
  end
end
```

# Capturing error

```ruby
begin
  person = Person.new("")
rescue => e
  puts e.class
end

begin
  puts 10 / 0
rescue ZeroDivisionError
  puts "don't divide by zero"
rescue => e
  puts e.class
end


class BadDataException < RuntimeError
end

begin
   raise BadDataException, "bad data"
  puts "don't divide by zero"
rescue => e
  puts e.class
end
```

# Catching Error

```ruby
catch(:done) do
  1000.times do 
    x = rand(1000)
    throw :done if x == 123
  end
  puts "Generated 1000 random numbers without generating 123"
end
```
