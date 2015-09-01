---
layout: post
title:  "Class Methods and Variables in Ruby"
date:   2015-08-17 09:00:00
categories: "programming"
---

Class methods are methods that apply to a particular class in Ruby. Rather than acting on a particular instance of a class, they act on the class blueprint itself, i.e. the instance of the Class object.

Class methods can't access instance variables. But instance methods can access class variables.

The most common way to create a class method in Ruby is to use the `self` keyword. This refers back to the class object itself.

```ruby
class IceCream
  @@total_scoops = 0

  def self.increment_scoops
    @@total_scoops +=1
  end

  def self.scoops_served
    @@total_scoops
  end
end
```

In this example, we use the class variable `@@scoops` to keep track of total ice cream scoops served. If you aren't careful, class variables can cause you problems in Ruby. Consider the following example.

```ruby
class FrozenYogurt < IceCream
  @@total_scoops = 0
end
```

What would you expect the output to be when you ran the following code?

```ruby
puts "Serving ice cream."
IceCream.increment_scoops
puts "#{IceCream.scoops_served} scoops of ice cream served."

puts "Serving froyo."
FrozenYogurt.increment_scoops
puts "#{FrozenYogurt.scoops_served} scoops of froyo served."
```

The answer is...

```
Serving ice cream.
1 scoops of ice cream served.
Serving froyo.
2 scoops of froyo served.
```

In Ruby, classes share class variables with their ancestors. Both of these classes are operating on the same `@@scoops variable`. This is often not the desired behavior. When you don't want this, you should use what are sometimes called "class instance variables". These are really just instance variables, but they're applied to the instance of the `Class` class, the blueprint object. You create one by defining an instance variable right in the class body. You can only refer to these variable within class methods. Let's try it.

```ruby
class IceCream
  @total_scoops = 0

  def self.increment_scoops
    @total_scoops +=1
  end

  def self.scoops_served
    @total_scoops
  end
end
class FrozenYogurt < IceCream
  @total_scoops = 0
end

puts "Serving ice cream."
IceCream.increment_scoops
puts "#{IceCream.scoops_served} scoops of ice cream served."

puts "Serving froyo."
FrozenYogurt.increment_scoops
puts "#{FrozenYogurt.scoops_served} scoops of froyo served."
```

This code outputs:

```
Serving ice cream.
1 scoops of ice cream served.
Serving froyo.
1 scoops of froyo served.
```

Now both of our class instances, `IceCream` and `Froyo`, each have their own `@scoops` variable. Remember, classes in Ruby are objects too, specifically instances of the `Class` class. It's a little confusing but all we are doing here is adding instance variables to our class instance. This avoids the issue with class variables being inherited by child classes.

