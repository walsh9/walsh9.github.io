---
layout: post
title:  "Fun with Enumerable#map"
date:   2015-08-03 09:00:00
categories: "programming"
---

Ruby's `map` function is great when you want to transform every item of a list in the same way. Here's the syntax from the Ruby docs:

```
map { |obj| block } → array
```

`map` iterates through an enumerable object, and returns an array using the return value of the code in `block` for each item in the enumberable. The `obj` is whatever the enumerable object supplies for iteration. For an array it will be a value in the array. For a hash it will be a key-value pair.

`map` is a non-destructive function. It leaves your original object alone and returns a new transformed object. You can transform your items in all sorts of ways. It's great when you have a set of data that's just a step or two away from what you want.

Add one to every item.

```ruby
[0, 5, 9].map {|value| value + 1}
#=> [1, 6, 10]
```

Get the first ten square numbers.

```ruby
(1..10).map {|n| n * n}
#=> [1, 4, 9, 16, 25, 36, 49, 64, 81, 100]
```

Capitalize every string.

```ruby
["hello", "world"].map {|word| word.to_s.upcase}
#=> ["HELLO", "WORLD"]
```




Simple Pig Latin with map.

```ruby
["ruby", "is", "fun"].map {|word| 
    vowels = ["a","e","i","o","u"]
    if vowels.include? word[0]
        word + "yay"
    else
        word[1..-1] + word[0] + "ay"
    end
}
#=> ["ubyray", "isyay", "unfay"]
```

You can also use `map` on hashes. Just remember `map` always returns an array, so you have to do a little bit of extra work to change a hash to a new hash with `map`.

Map always returns an array, even when applied to a hash.

```ruby
balances = {"Amy" => 20000.0, "Bill" => 4000.0, "Carol" => 6000.0}
interest_rate = 1.01
balances.map {|_, value| value * interest_rate]}
#=> [20200.0, 4040.0, 6060.0]
```

When you return key-value pairs, you still get an array.

```ruby
balances.map {|key, value| [key, value * interest_rate]}
#=> [["Amy", 20200.0], ["Bill", 4040.0], ["Carol", 6060.0]]
```

You can convert an array of key-value pair arrays to a hash using `.to_h`

```ruby
balances.map {|key, value| [key, value * interest_rate]}.to_h
#=> {"Amy"=>20200.0, "Bill"=>4040.0, "Carol"=>6060.0}
```

I hope these examples helped you to better understand what the `map` function does and how to use it.