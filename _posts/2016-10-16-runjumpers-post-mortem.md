---
layout: post
title:  "Runjumpers Post-mortem"
layout: post
date: 2016-10-16
categories:
  - games
---

I made a game for [GBJAM 5](https://itch.io/jam/gbjam-5) called [Runjumpers](https://walsh9.itch.io/runjumpers). It's an action jumping game with a 4 color palette for the graphics. Here's a few interesting things I learned while making it.

### Game designy stuff

#### Music is important

I knew it would eat up a lot of my limited time, since I'd never done it before, so I decided in advance to not add any music. But half of all the feedback I've gotten so far has mentioned that it would be nice if the game had music.

So I've been looking into how to make music. I don't ever expect to make a masterpiece, but being able to create some passable catchy tunes will come in handy for future game jams.

I'm planning on a post-jam update for the game with some music. So far, I've only got this track for the title screen.  Making something suitable for the running part has proven trickier.  I'm gonna keep trying though.

<iframe width="100%" height="166" scrolling="no" frameborder="no" src="https://w.soundcloud.com/player/?url=https%3A//api.soundcloud.com/tracks/288479065&amp;color=ff5500&amp;auto_play=false&amp;hide_related=false&amp;show_comments=true&amp;show_user=true&amp;show_reposts=false"></iframe><br/>

#### Small gameplay changes can make a big difference

When I first started making the game it only had one jump key, and you could only jump one height. I thought about having a variable height jump based on how long you pushed the key, but first I tried just adding a hop key for small jumps. The game instantly became much more interesting and challenging.

I played around and started building levels based on choosing between hop and jump. As I tested them I would get frustrated and think things like, "Oh come on! I almost had it... Just one more try and I'll get past that part!" I was having fun. This was working.

So this change only increased the available player choices at any given moment from 2 (jump / don't jump) to 3. Sure that's still a 50% increase in complexity, but it's also the smallest change possible. Sometimes that's all you need.

### Technical JavaScripty stuff

#### JavaScript at 60 Frames Per Second is tricky

I was getting some lag when testing my game in Firefox on a different computer. After some investigation I found one interesting place for optimization.

I don't usually worry about the details of garbage collection when writing JavaScript. It's just something that happens automatically. But when you only have 16.6ms to update each frame, any garbage collection step that takes longer than that means dropped frames and choppy animation. Now, modern browsers are actually pretty good at scheduling garbage collection between frames, but it can still add up quickly and slower or busier machines can still fall behind.

How do we reduce garbage collection? Just reduce the amount of garbage we create. What is garbage exactly? In this case we mean creating objects that are never used again. The browser has to do some computation to free up that memory.

[Here's a great stackoverflow answer with a list of things that cause browsers to allocate memory.](http://stackoverflow.com/a/18411275)

So for example:

```js
update() {
  //...
  player.pos = { x: newX, y: newY };
  //...
}
```

Whoops we just created a new throwaway object every time our update code runs.

```js
update() {
  //...
  player.pos.x = newX;
  player.pos.y = newY;
  //...
}
```

Much better.

In general, instead of creating new objects during the game loop, create your objects at init time and make changes to those.

Here's a profile of 6 seconds of gameplay in Chrome from before I refactored to avoid this.

![Screenshot of a graph of JavaScript heap allocation showing dozens of jaggy sawtooths spread over 6 seconds](/i/gc-before.png)

And here's [after](https://github.com/walsh9/runjumpers/commit/19cdc6562f6feb9f8b4e338995dbace3a0203a51).

![Screenshot of a graph of JavaScript heap allocation showing only two smooth increases and sharp drops spread over 6 seconds](/i/gc-after.png)

Check out those heap allocation graphs. Also notice 'Minor GC' drops from 17.3ms to 0.4ms. And this is just a simple running game with no enemies or items. In a game with bullets and enemies flying around the difference would even be more dramatic.

### KeyboardEvent.key is cool

[Modern KeyboardEvents](https://www.w3.org/TR/uievents-key/) are great.

Instead of something like this:

```js
window.addEventListener('keydown', function(event) {
  if (event.keyCode === 38) { // Up
    player.jump();
  }
});
```
<br/>
we can write this:

```js
window.addEventListener('keydown', function(event) {
  if (event.key === 'UpArrow') {
    player.jump();
  }
});
```

Unfortunately this isn't currently supported by Safari, but that can be fixed with a [polyfill](https://github.com/cvan/keyboardevent-key-polyfill).

One more issue is that Edge uses some non-standard key names (still not fixed since IE9!), so you will actually have to write:

```js
window.addEventListener('keydown', function(event) {
  if (event.key === 'UpArrow' || event.key === 'Up') {
    player.jump();
  }
});
```

Check the footnotes [here](https://developer.mozilla.org/en-US/docs/Web/API/KeyboardEvent/key/Key_Values) for more details on those.

Even with these drawbacks, it's still a lot nicer than littering your code with arcane keyCode numbers.

### Don't forget to play the game

[https://walsh9.itch.io/runjumpers](https://walsh9.itch.io/runjumpers)


