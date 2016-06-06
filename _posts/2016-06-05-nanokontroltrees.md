---
layout: post
title:  "Trees and nanoKONTROL"
layout: post
date: 2016-06-05
categories:
  - projects
---
A few days ago, I got a KORG nanoKONTROL2 to play with.  It's supposed to be for music stuff, but I just like all the sliders and dials.

I wanted to hook this up to my [fractal tree stuff](https://github.com/walsh9/topiary) to control a little forest with all the sliders and dials. The demos folder for my tree library was getting a little bloated so I wanted to break out the demos into their own repo first. And to do this properly I decided to convert the library from just a script that creates a global object into an npm module. I settled on webpack with [babel-loader](https://github.com/babel/babel-loader) to pack things up. I decided to go with babel-loader so I could use the ES6 module syntax.

One thing I got hung up on while trying to get this setup working was when I couldn't figure out why my module was only exporting an empty object. And when I tried to use it I just got lots of `foo is undefined` errors.  It turns out you can't just `export default` something from your main file and expect webpack to know what to do. You actually have to configure webpack to export a module. Eventually, I set up the [appropriate config values](https://github.com/walsh9/topiary/blob/master/webpack.config.js#L15-L17), got all the demos working off the module, and moved them into a [new repo](https://github.com/walsh9/topiary-demos).

With that done it was time to get ready to hook up the nanoKONTROL2. Now, by default, the trees that come out of my library can have a lot of randomness, which isn't good for smooth animated transitions between values.  But a while back I made a [creepy animated tree](https://walsh9.github.io/topiary-demos/animation/) with a function that is constrained to only creating deterministic trees. It had a nice simple interface where you just pass in an array of numbers with values between 0 and 1 and you get a tree.  This was inspired by ideas from [Kate Compton's](https://twitter.com/GalaxyKate) [ProcJam 2015 Talk](https://youtu.be/s_eyo_m_hnc?t=958). 

So now I just had to hook up the values from the sliders and dials to some trees. I used [this excellent library](https://github.com/shokai/korg-nano-kontrol) to do most of the hard work there. And here's the result.

<iframe width="560" height="315" src="https://www.youtube.com/embed/8QnNRrv1Xkk" frameborder="0" allowfullscreen></iframe><br>

If you have your own nanoKONTROL or nanoKONTROL2 you can [try it yourself](https://walsh9.github.io/topiary-demos/nanokontrol/index.html) in any browser that supports webMIDI. (please plug in your device before loading the page.)
