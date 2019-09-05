```ruby
params = nil
# Bad.
params[:name][:age]
# NoMethodError (undefined method `[]' for nil:NilClass)

# Better, use dig to extract nested value. Dig will return nil if the value is not found.
val = params.dig(:name, :age) # Equivalent to params && params[:name] && params[:name][:age].
val.blank? # => true
val.nil? # => true

# Provide default with dig. 
params.dig(:name, :age) || ''

# .fetch method allows defaults, but can only fetch one level at a time.
params.fetch(:name).fetch(:age, 1)
```
