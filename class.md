# Classes and Inheritance

```ruby
class Shape
end

class Square < Shape
  def initialize(side_length)
    @side_length = side_length

    if defined?(@@number_of_squares)
      @@number_of_squares += 1
    else
      @@number_of_squares = 1
    end
  end

  def self.count
    @@number_of_squares
  end

  def area
    @side_length * @side_length
  end

  def perimeter
    @side_length * 4
  end

  # Class method.
  def self.perimeter(side_length)
    side_length * 4
  end
end

class Triangle < Shape
  def initialize(base_width, height, side1, side2, side3)
    @base_width = base_width
    @height = height
    @side1 = side1
    @side2 = side2
    @side3 = side3
  end

  def area
    @base_width * @height / 2
  end

  def perimeter
    @side1 + @side2 + @side3
  end
end

square = Square.new(2)
puts square.area
puts square.perimeter

_square = Square.new(4)
puts Square.count
puts Square.perimeter(3)
```


## Private 
```ruby
class Person
  def initialize(name)
    set_name(name)
  end

  def set_name(name)
    first, last = name.split
    set_first_name(first)
    set_last_name(last)
  end

  def name
    [@first_name, @last_name].join(' ')
  end

private
  def set_first_name(name)
    @first_name = name
  end

  def set_last_name(name)
    @last_name = name
  end
# private :set_first_name, :set_last_name
end

person = Person.new("john doe")
puts person.name
person.set_name('johny slyvester')
# person.set_first_name('johny')
puts person.name
```

# Nested classes

```ruby
class Drawing
  def self.circle  
    Circle.new
  end

  class Line
  end

  class Circle
  end
end


puts Drawing.circle
puts Drawing::Circle.new
puts Drawing::Line.new
```

# The scope of constant

```ruby
Pi = 3.14

class OtherPlanet
  Pi = 4.5
  def self.circumference(radius)
    2 * Pi * radius
  end
end

puts Pi
puts OtherPlanet::Pi
puts OtherPlanet.circumference(10)
```
# Dungeon Adventure Game

```ruby
class Dungeon
  attr_accessor :player

  def initialize(player)
    @player = player
    @rooms = {}
  end

  def add_room(reference, name, description, connections)
    @rooms[reference] = Room.new(reference, name, description, connections)
  end

  def start(location)
    @player.location = location
    show_current_description
  end

  def show_current_description
    puts find_room_in_dungeon(@player.location).full_description
  end

  def find_room_in_dungeon(reference)
    @rooms[reference]
  end

  def find_room_in_direction(direction)
    find_room_in_dungeon(@player.location).connections[direction]
  end

  def go(direction)
    puts "You go " + direction.to_s
    @player.location = find_room_in_direction(direction)
    show_current_description
  end
end

# class Player
#   attr_accessor :name, :location

#   def initialize(player_name)
#     @name = player_name
#   end
# end
Player = Struct.new(:name, :location)
# Room = Struct.new(:reference, :name, :description, :connections)

class Room
  attr_accessor :reference, :name, :description, :connections

  def initialize(reference, name, description, connections)
    @reference = reference
    @name = name
    @description = description
    @connections = connections
  end

  def full_description
    @name + '\n\nYou are in ' + @description
  end
end

me = Player.new("John Doe")
dungeon = Dungeon.new(me)
puts dungeon.player.name
dungeon.add_room(:largecave, "Large cave", "a large cavernous cave", {:west => :smallcave})
dungeon.add_room(:smallcave, "Small cave", "a small claustrophobic cave", {:east => :largecave})

dungeon.start(:largecave)
dungeon.go(:west)
dungeon.go(:east)

# Struct is a special class that holds attributes only.
# Person = Struct.new(:name, :gender, :age)
# john = Person.new("john", "male", 50)
# jane = Person.new("jane", "female", 30)
# puts "#{john.name} #{john.age}"
# puts "#{jane.name} #{jane.age}"

```
