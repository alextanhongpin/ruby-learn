# Hashes

```ruby
dictionary = {'a' => 1, 'b' => 2, 3 => 4, 'A' => 5}
puts dictionary
puts dictionary['a']
puts dictionary['b']
puts dictionary['3']
puts dictionary[3]

dictionary.each { |key, value| puts "#{key} => #{value}" }
puts dictionary.keys.join(', ')
puts dictionary.values.join(', ')

puts dictionary.delete(3) # This will print out the value of the deleted key.
puts dictionary

puts dictionary.delete('z') # If the key does not exist, this will return nil.
puts dictionary

# Conditional delete, will return the remaining dictionary.
puts dictionary.delete_if {|key, value| value < 4}
puts dictionary
puts dictionary.key?(‘a’) # Checks if a key exists.
```
