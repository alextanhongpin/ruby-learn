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

# Don't rescue Exception

Do not do this. This will swallow every single exception, including errors when stopping the app, or syntax errors.

```ruby
begin
  do_something()
rescue Exception => e
  
end
```

Rescue `StandardError` instead. Both examples below are equivalent.

```ruby
begin
  do_something()
rescue StandardError => e
  # Only app exceptions are swallowed. Things like SyntaxError are left alone.
end

begin 
  do_something()
rescue => e
  # This is the same as rescuing StandardError.
end
```

# CustomExceptions

CustomExceptions should inherit from StandardError.

```ruby
class SomethingBad < StandardError
end

raise SomethingBad
```

# Example of custom errors

Context: We have an image upload service, and we want to handle errors for the following conditions:
- when the image is too large
- when the image is too small
- when the image format is not JPEG

```ruby
class ImageHandler
  def self.handle_upload(image)
      raise 'Image is too big' if image.size > 10.megabytes
      raise 'Image is too small' if image.size < 100.kilobytes
      raise 'Image is not a JPEG' unless %w[JPG JPEG].include?(image.extension)
      
      # Do stuff.
  end
end
```

After refactoring:

```ruby
class ImageHandler
  class ImageExtensionError < StandardError; end
  class ImageSizeError < StandardError; end
  class ImageTooLargeError < ImageSizeError
    def message
      'Image is too large'
    end
  end
  
  class ImageTooSmallError < ImageSizeError
    def message
      'Image is too small'
    end
  end
  
  def self.handle_upload(image)
      raise ImageTooLargeError if image.size > 10.megabytes
      raise ImageTooSmallError if image.size < 100.kilobytes
      raise ImageExtensionError unless %w[JPG JPEG].include?(image.extension)
      
      # Do stuff.
  end
end

class ImageUploadController < ApplicationController
  def upload
    @image = params[:image]
    ImageHandler.handle_upload(@image)
    
    redirect_to :index, :notice => 'Image upload success!'
  rescue ImageHandler::ImageSizeError => e
    render 'edit', :alert => "Error: #{e.message}"
  rescue ImageHandler::ImageExtensionError
    head :forbidden
  end
end
```


# References
- https://www.honeybadger.io/blog/ruby-exception-vs-standarderror-whats-the-difference/

  puts e.class
