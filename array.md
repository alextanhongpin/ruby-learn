
# Array

```ruby
x = [1, 2, 3, 4, 99]
puts "length is: #{x.length}"
puts x[0] # Access the head.
puts x.first
puts x[-1] # Access the tail.
puts x.last
puts x.first(2).join(', ')
puts x[-1000] == nil # Out of index returns nil.
puts x[1000].nil? 
puts x.include?(1)
puts x.include?(100)
puts x.reverse.join(', ')

x[0] += 1 # Modify an item in an array.
puts x.join(', ') # Join the array.

x << 200 # Append to array.
puts x.join(', ')
puts x.pop
puts x.join(', ')

y = []
puts y.pop.nil?
puts y.empty?
```

# These are aliases.

```ruby
puts x.map {|n| n * 2}.join(', ')
puts x.collect {|n| n * 2}.join(', ')
z = [1] * 10
puts z.join(', ')
puts (x+z).join(', ')
puts (x-z).join(', ')
```

# Filtering with select

```ruby
x = [1, 2, 3, 4]
puts x.select{|n| n > 2}.join(', ')

x = [1, 2, 3, 4].reverse

# Sorting.
puts x.sort.join(', ')
puts x.sort_by {|n| 10 - n}.join(', ')

# Slicing.
puts x[0..1].join(', ')
puts x[0...1].join(', ')
```

