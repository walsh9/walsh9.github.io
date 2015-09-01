---
layout: post
title:  "Slicing and Splicing: Ruby and Javascript Gotchas"
date:   2015-08-24 09:00:00
categories: "programming"
---

Ruby and Javascript both have a method called `slice`. They looks similar but they work differently. Let's look at some examples.

Guess what the following Ruby code returns.

```ruby
[1,2,3,4,5].slice(0,2)
```

And it returns...

`[1,2]`

It's a new array containing the first `2` values of the calling array starting from index `0`.

What about this Javascript?

```javascript
[1,2,3,4,5].slice(0,2);
```

`[1,2]`

Javascript returns an array with the values starting from index `0` up to, but not including index `2`.

I know. It looks the same. But don't fall for it. Here's another example that actually shows this difference.

Ruby

```ruby
[1,2,3,4,5].slice(2,3)
```

`[3, 4, 5]`

Javascript

```javascript
[1,2,3,4,5].slice(2,3);
```

`[3]`

In Ruby the method is `slice(start, length)` where `start` is the starting index, `length` is the number of values to take up to.

In Javascript the method is `slice(begin, end)` where `begin` is, again, the starting index, but `end` is the index to take up to, non-inclusive.

`slice` also has a single argument format

Ruby

```ruby
[1,2,3,4,5].slice(2)
```

`3`

Javascript

```javascript
[1,2,3,4,5].slice(2);
```

`[3, 4, 5]`

Here, Ruby's `slice(index)` simply returns the value at `index`.

And Javascript's `slice(begin)` returns a new array starting from the value at the index `begin` all the way through to end of the array.

Ruby and Javascript both also have `String.slice` that work the same as their respective array-based counterparts, but on characters in the string.

Ruby

```ruby
"hello".slice(2)
"hello".slice(2,3)
```

```
"l"
"llo"
```

Javascript

```javascript
"hello".slice(2);
"hello".slice(2,3);
```

```
"llo"
"l"
```

Javascript also has a `splice` method. It's just like `slice` but it removes the selected values from the original array. It's like Ruby's `slice!` method.

Ruby

```ruby
arr = [1,2,3,4,5]
arr.slice!(1,1)     # returns  [2]
arr                 # contains [1,3,4,5]
```

Javascript

```javascript
arr = [1,2,3,4,5];
arr.splice(1,1);     // returns  [2]
arr;                 // contains [1,3,4,5]
```

Okay last example.

Ruby

```ruby
str = "hello"
str.slice!(1,1)     # returns  "e"
str                 # contains "hllo"
```

Javascript

```javascript
str = "hello";
str.splice(1,1);
```

`TypeError: str.splice is not a function`

Whoops! There's no built-in String.splice method in Javascript. Arrays only!

If you have to switch between Ruby and Javascript a lot, be careful out there and always keep you methods straight.

And there are more differences than what I mentioned here. Ruby's `slice` methods can take a _range_ value as a parameter. Javascripts `splice` can be used to _insert_ values. And more! Check out the docs for details.

## References

*   [Ruby Array#slice Documentation](http://ruby-doc.org/core-2.2.0/Array.html#method-i-slice)
*   [Ruby String#slice Documentation](http://ruby-doc.org/core-2.2.0/String.html#method-i-slice)
*   [Ruby Array#slice! Documentation](http://ruby-doc.org/core-2.2.0/Array.html#method-i-slice-21)
*   [Ruby String#slice! Documentation](http://ruby-doc.org/core-2.2.0/String.html#method-i-slice-21)
*   [Javascript Array.prototype.slice() Documentation](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/slice)
*   [Javascript String.prototype.slice() Documentation](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/slice)
*   [Javascript Array.prototype.splice() Documentation](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/splice)