# Dates and Time

Extending the Integer to support time operations:
```ruby
class Integer
  def seconds
    self
  end

  def minutes
    self * 60
  end

  def hours
    self * 60 * 60
  end

  def days
    self * 60 * 60 * 24
  end
end
```


## Operations

```ruby
puts 10.minutes
puts Time.now
puts Time.now.to_i # Convert to unix timestamp.
puts Time.at(Time.now.to_i)
puts Time.now + 10.minutes
```

## Format

```ruby
year = 2019
month = 1 # Ranges from 1-12. Will throw error if out of range.
day = 1
hour = 12
min = 57
sec = 0
msec = 0
puts Time.local(year, month, day, hour, min, sec, msec)
puts Time.local(year, month, day, hour, min, sec, msec)
puts Time.local(2019)
puts Time.gm(2019)
puts Time.gm(2019).gmt?
puts Time.utc(2019)
puts Time.utc(2019).utc?

t = Time.now
puts [t.year, t.month, t.day].join('-')
```
