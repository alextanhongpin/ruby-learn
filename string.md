# String Operations

```ruby
str = "hello world"

puts str.upcase
puts str.downcase
puts str.capitalize
puts str.chop
puts str.next
puts str.reverse
puts str.sum
puts str.swapcase
puts str.upcase.reverse.next
```

# Bracket

```ruby
5.times { puts "hello world" }
5.times do puts "hello world" end
```

# Looping

```ruby
5.downto(1) { |n| puts "down to: #{n}"}
0.step(50, 5) { |n| puts "step: #{n}" }
1.upto(5) { |n| puts "up to: #{n}"}
(1..5).each { |n| puts "inclusive: #{n}" } # Same as above.
(1...5).each { |n| puts "exclusive: #{n}" }
```
We can omit the parameters if it is not required.

```ruby
5.downto(1) { puts "down to: #{n}"}
0.step(50, 5) { puts "step: #{n}" }
1.upto(5) { puts "up to: #{n}"}
(1..5).each { puts "inclusive: #{n}" } # Same as above.
(1...5).each { puts "exclusive: #{n}" }
```

# Division
```ruby
puts 10 / 3 # Produces an integer.
puts 10.0 / 3 # If either one of the numerator or denumerator is a float, it will return a float.
puts 10 / 3.0
```

# Conversion

```ruby
puts 1.to_s.class
puts "1".to_i.class
puts "1".to_f.class

char = "a"

# If the string cannot be converted to a character,
# it will produce 0.
puts char.to_i
puts char.to_i.class
```

# Multiline

```
text = %q{
  this is a multiline
  string
}
puts text

text = %q!
  the delimiter can be 
  anything
!
puts text


text = %q=
  the delimiter can be 
  anything
=
puts text

text = <<END
  this also 
  works
END

puts text
```


## Characters
```ruby
puts "abc" * 5
puts "a" > "b"
puts "a" < "b"
puts "a" <=> "b"
puts "a".ord
puts "A".ord
puts 97.chr
```

## String concatenation

```ruby
str = "hello"
str << " "
str << "world"
puts str
```

# Substitutions
```ruby
puts "foobar".sub("foo", "bar") # Replace foo with bar.
puts "foofoo".sub("foo", "bar") # Replace the first foo with bar.
puts "foofoo".gsub("foo", "bar") # Replace all foo with bar.
puts "FooFoo".gsub("foo", "bar") # Case-sensitive, no foo is replaced.
puts "FooFoo".gsub(/foo/i, "bar") # Replace all foo, ignoring capitalization.
```

# Iterations with regular expression

```ruby
# Scan a single character at a time.
"xyz".scan(/./){ |letter| puts letter }

# Scan two characters at a time.
"xyz".scan(/../){ |letter| puts letter }
"abcde".scan(/../){ |letter| puts letter }

# This includes whitespaces.
"hello world".scan(/../){ |letter| puts letter }
# ...which we can omit.
"hello world".scan(/\w\w/){ |letter| puts letter }

# Capture the cost.
"the car costs $1000".scan(/[0-9]+/) { |n| puts n }

# Capture vowels.
"the car costs $1000".scan(/[aeiou]/) { |c| puts c }
```

## Matching

```ruby
puts "Strings has vowels" if "this is a test" =~ /[aeiou]/

# Returns the index of the character e.
puts "this", "none" =~ /[e]/

cost = "the car costs $1000".match(/[0-9]+/)
puts cost, cost.class, cost[0], cost.length
```
