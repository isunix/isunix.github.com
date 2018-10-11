---
layout: post
title: "tap method in ruby"
date: 2015-07-20 15:31:51 +0800
comments: true
categories: Ruby
---
There is a "tap" method in Ruby and I find it is very useful.

The definitionof "tap" in ruby documentaion is:

```
Yields self to the block, and then returns self. The primary purpose of this method is to “tap into” a method chain, in order to perform operations on intermediate results within the chain.
```

Put it anonther way:

```
It’s a helper for call chaining. It passes its object into the given block and, after the block finishes, returns the object:
```

```ruby
an_object.tap do |o|
  # do stuff with an_object, which is in o
end # ===> an_object
```

Another example:

```ruby
def hash_table(numbers, target)
    [].tap do |result|
      hash = {}
      numbers.each_with_index do | n, i |
        if j = hash[target - n]
          return result << j + 1 << i + 1
        end
        hash[n] = i
      end
    end
  end
```