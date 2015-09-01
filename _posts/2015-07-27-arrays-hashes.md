---
layout: post
title:  "Arrays and Hashes"
date:   2015-07-27 09:00:00
categories: "programming"
---

Ruby has two commonly used data types for storing lists of objects. The array and the hash.

## Arrays

An array is a collection of objects with numbered indexes starting at zero. A common way to think of arrays is a row of numbered buckets. Each bucket is labeled with a number in order starting from zero and they can all contain one object. This can be any object including things like numbers, strings, the nil object, and even other arrays.

They're useful for simple lists of things, both ordered and unordered.

    "Bread"   "Eggs"   "Milk"   "Tea" "Cheez-Its"
       |        |        |        |        |
     __v__    __v__    __v__    __v__    __v__ 
    |_____|  |_____|  |_____|  |_____|  |_____|
    |__0__|  |__1__|  |__2__|  |__3__|  |__4__|
     \___/    \___/    \___/    \___/    \___/ 


To create an empty array:

```ruby
my_array = []
# or
my array = Array.new()
```

To create an array with contents:

```ruby
my_array = ["Bread", "Eggs", "Milk", "Tea", "Cheez-Its"]
```

Add items to an array

```ruby
my_array << "Cashews"
# or
my_array.push("Ice Cream")
```

Reference items in an array

```ruby
my_array[3] # Get the item in bucket 3
```

## Hashes

Hashes are similar to arrays, but instead of each item being assigned to a numbered bucket, it's assigned a key. What's a key? Well a key can also be any object, but for most cases you would use a string. It's like an array where you get to name the buckets.

Hashes are good for groups of organized data, where each value has a name.

      "Matt"     11.5         2     
        |          |          |      
     ___v___    ___v___    ___v___  
    |_______|  |_______|  |_______| 
    |_"Name"|  |_"Shoe"|  |_"Feet"|
     \_____/    \_____/    \_____/ 

They're also great for 'dictionaries' where you want to link one set of values to another.

      "Ottowa"     "Dublin"     "Paris"      "Tokyo" 
         |            |            |            |
     ____v____    ____v____    ____v____    ____v____
    |_________|  |_________|  |_________|  |_________|
    |_"Canada"|  |"Ireland"|  |_"France"|  |_"Japan"_|
     \_______/    \_______/    \_______/    \_______/  

To create an empty hash:

```ruby
my_hash = {}
# or
my hash = Hash.new()
```

To create a hash with contents:

```ruby
my_hash = {
    "Canada" => "Ottowa",
    "Ireland" => "Dublin",
    "France" => "Paris",
    "Tokyo" => "Japan"
}
```

Add items to an hash

```ruby
my_hash["United States"] = "Washington D.C."
# or
my_array.store("Germany", "Berlin")
```

Reference items in an array


```ruby
my_hash["Canada"] # Get the item from the bucket with the key "Canada"
# or
my_hash.fetch("Ireland")
```