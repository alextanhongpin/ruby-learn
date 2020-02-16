## Diff

When dealing with many-to-many, we sometimes need to figure out what needs to be deleted, or added. 

```ruby
old = [1,2,3]
new = [1,2]

to_remove = old - new
to_add = new - old

p to_remove, to_add
```
