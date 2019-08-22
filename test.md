## Testing

```ruby
require "minitest/autorun"

class TestTitleSize < Minitest::Test
  def test_basic
    assert_equal(1, 1)
    assert(true)
    refute_equal(1, 0)
    # assert_raise(ZeroDivisionError) {2/0}
    assert_instance_of(Integer, 1)
    # flunk()
  end
end
```
