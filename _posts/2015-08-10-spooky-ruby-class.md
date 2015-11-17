---
layout: post
title:  "A Spooky Ruby Class"
date:   2015-08-10 09:00:00
categories: "programming"
---

In Ruby, pretty much everything is an object. The number `5` is an object. The string "boo!" is an object. When we want to be able to create a lot of similar objects, we use classes. Classes are objects too.

A class is like a blueprint for something we call instances. Each object you create using a class is called an instance. Ruby has a lot of built-in classes. Let's take a quick look at the `String` class. To create a new instance of any class, we call the `new` method. So to create instances of the `String` class we could type:

```ruby
greeting = String.new("Hi!")
#=>"Hi!"
formal_greeting = String.new("Hello!")
#=>"Hello!"
```

These `String` instances are each their own objects but they also share a lot of methods that they get from the `String` class.

```ruby
greeting.size
#=>3
formal_greeting.size
#=>6
```

The built-in classes are great and all, but let's try making our own. Let's make a class for spooky monsters.

```ruby
class Monster
  def initialize(spookiness, spooky_grabber)
    @spookiness = spookiness
    @spooky_grabber = spooky_grabber
  end
end
```

A lot of stuff is actually going on here so let's break it down a bit.


```ruby
class Monster
```

The `class` keyword declares the beginning of a class. Our class can be referenced later by its class name, `Monster`.

``ruby
  def initialize(spookiness, spooky_grabber)
```

Here we declare the `initialize` method. `initialize` is a special method. Whenever a new instance is of a class created, that class's `initialize` method is automatically called on that instance. It also receives all the arguments that were passed to the new method. This is the place to set up your object.

```ruby
    @spookiness = spookiness
    @spooky_grabber = spooky_grabber
```

Just assigning the parameters to some variables. But what are those @ signs? Those @ signs indicate that these are instance variables. Each instance keeps track of it's own instance variables. Each monster will have it's own individual spookiness and spooky grabber.

Now we can create some instances!

```ruby
ghost = Monster.new(1, "a chilling presence")
skeleton = Monster.new(2, "a bony claw")
fishman = Monster.new(2, "a damp webbed hand")
cthulu = Monster.new(3, "several eldritch tentacles")
```

The good news is we have our instances. The bad news is, they don't really do much yet. Let's add some methods to our class so we can at least inspect the values we set up.

```ruby
class Monster
  def initialize(spookiness, spooky_grabber)
    @spookiness = spookiness
    @spooky_grabber = spooky_grabber
  end

  def spookiness
    @spookiness
  end

  def spooky_grabber
    @spooky_grabber
  end
end
```

We can use these methods to see the values of our instance variables.

```ruby
ghost.spookiness
#=>1
```

That seems like a lot of code to write just to read each variable. I know what you're thinking. This is Ruby. There's gotta be a shorter way. That's where the `attr_reader` keyword come into play.

```ruby
class Monster
  attr_reader "spookiness"
end
```

is the same as

```ruby
class Monster
  def spookiness
    @spookiness
  end
end
```

Great let's add it to our code.

```ruby
class Monster
  attr_reader "spookiness", "spooky_grabber"
```

And let's add some methods to print spooky text to the console.

```ruby
class Monster
  attr_reader "spookiness", "spooky_grabber"

  def initialize(spookiness, spooky_grabber)
    @spookiness = spookiness
    @spooky_grabber = spooky_grabber
  end

  def spook
    print "You suddenly feel #{@spooky_grabber} brush your shoulder"
    puts  "." * spookiness
  end

  def scare
    print "You suddenly feel #{@spooky_grabber} wrap around your neck"
  puts  "!" * spookiness
  end
end
```

The `spook` and `scare` methods are called 'instance methods'. That's because each instance can use them. And when you call an instance method it has access to its caller's instance variables.

```ruby
ghost.spook
#  You suddenly feel a chilling presence brush your shoulder.
#=>nil
skeleton.scare
#  You suddenly feel a bony claw wrap around your neck!!
#=>nil
```

Sometimes you have a method that's related to a class, but doesn't really apply to individual instances. You can create 'class methods' by using the `self` keyword. Here's an example. Pay attention to how `self` is used.

```ruby
class Monster
  def self.merge (monster_a, monster_b)
    spookiness = monster_a.spookiness + monster_b.spookiness
    grabber = monster_a.spooky_grabber + " and " +  monster_b.spooky_grabber
    Monster.new(spookiness, grabber)
  end
end
```

You call class methods like this:

```ruby
spook_team = Monster.merge(fishman, cthulu)
```

This method combines the properties of two objects then creates and returns a new instance. The created instance also has all the same methods as the other instances.

```ruby
spook_team.scare
#  You suddenly feel a damp webbed hand and several eldritch tentacles wrap around your neck!!!!!
#=>nil
```

Great, nice and spooky!

And here's the full code for our class.

```ruby
class Monster
  attr_reader "spookiness", "spooky_grabber"

  def initialize(spookiness, spooky_grabber)
    @spookiness = spookiness
    @spooky_grabber = spooky_grabber
  end

  def spook
    print "You suddenly feel #{@spooky_grabber} brush your shoulder"
    puts  "." * spookiness
  end

  def scare
    print "You suddenly feel #{@spooky_grabber} wrap around your neck"
    puts  "!" * spookiness
  end

  def self.merge (monster_a, monster_b)
    spookiness = monster_a.spookiness + monster_b.spookiness
    grabber = monster_a.spooky_grabber + " and " +  monster_b.spooky_grabber
    Monster.new(spookiness, grabber)
  end
end
```