## Threads

```ruby
threads = []
10.times do
  thread = Thread.new do
    10.times {|i| print i; $stdout.flush; sleep rand(2) }
  end

  threads << thread
end

threads.each{|thread| thread.join}
```
## Fiber 
```ruby
sg = Fiber.new do
  s = 0 
  loop do
    square = s * s
    Fiber.yield square
    s += 1
  end
end

10.times { puts sg.resume }
```
## Passing data to Fiber
```ruby
sg = Fiber.new do
  s = 0 
  loop do
    square = s * s
    s += 1
    s = Fiber.yield(square) || s
  end
end

puts sg.resume
puts sg.resume 10
puts sg.resume 5
puts sg.resume
```
