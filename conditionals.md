# Conditionals

```ruby
n = 10
if n < 10
  puts "less than 10"
elsif n == 10
  puts "equals 10"
else
  puts "greater than 10"
end
```

# Assigning the conditional to variables
```ruby
out = if n < 10
        "less"
      else
        "greater or equal"
      end
puts out
```

# Ternary operator

```ruby
out = n < 10 ? "less" : "greater"
puts out

n = 1100
out = case n 
        when 1...10 
          "less"
        when 10
          "equal"
        else 
          "more"
      end
puts out
```

# Code blocks

```ruby
def each_vowel(&code_block)
  %w{a e i o u}.each{|char| code_block.call(char) }
end

puts "with code block:"
each_vowel {|vowel| print vowel }
puts 

def each_vowel
  %w{a e i o u}.each{|char| yield char }
end

puts "with yield:"
each_vowel {|vowel| print vowel }
```

# Lambda

```ruby
print_to_screen = lambda { |x| puts x }
print_to_screen.call(100)
```
