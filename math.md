# Round to nearest 0.5 in Ruby

```ruby
class Float
  def round_to_half
    (self * 2.0).round / 2.0
  end
end

1.7.round_to_half
```
