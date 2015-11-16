---
title: Looking back on the development of Super Micro Paint
author: walsh9
layout: post
permalink: /projects/looking-back-on-super-micro-paint
categories:
  - notes
  - projects
---
About a month ago, I finished a minimalist pixel animation web app I was working on called Super Micro Paint. It lets you create 4 frame, 2 color, 32&#215;16 pixel animations really quickly. Then you can turn your creations into gifs that resemble things like LCDs, LEDs, plastic toy blocks, and more. I didn&#8217;t make any sort of detailed post when I launched it, but here&#8217;s something now.

**Remember Tamagotchi?**

I wanted to make it this really minimalist thing without being trivial. A big inspiration here came from Tamagotchi virtual pets. The original Tamagotchi only had a 32&#215;16 pixel, 2 color display, but it was still able to show all sorts of wonderful little animated creatures. I used those same dimensions for Super Micro Paint.

And then there was Mario Paint. I spent a lot of time with it when I was a kid and I loved how easy it was to make animations. Actually, I had an idea early on to make SMP more Mario Paint-like, with all sorts of fun sounds and animated screen clear effects but I decided to keep things simple.

Surprisingly, I had <i>not</i> heard about the Etch-a-Sketch Animator until this was almost finished. I mean, literally one day before I made the first complete version of this public, I saw the Etch-a-Sketch animator on Wikipedia and said &#8216;huh.&#8217;

**An Old Cheap LCD Toy**

I wanted to simulate the experience of an old LCD toy from an alternate history 1990s. Maybe it was buried at the bottom of a box in the closet that never noticed before. Maybe you found it in a mysterious thrift shop that you could never manage to locate again. Anyway, I wanted it to really look and function just like a cheap old LCD display. This meant I could only add as many icons as would fit on the screen. And each icon (or pixel) could only be on or off. There was no room for shades of grey or overlapping display elements.

Sticking firmly to this idea sometimes limited the features I could include. For example, since I couldn&#8217;t use transparency or gray pixels, I couldn&#8217;t include an onion skinning mode. And I had to implement the indicators for dragging out lines and shapes by blinking a shadow of the pixels. I also didn&#8217;t want to include out of place things like &#8216;hyperlinks&#8217; or &#8216;tooltips&#8217;, so I made a manual in the style of an instruction sheet just you might find with an old toy.

I don&#8217;t think these limitations were a bad thing. Whenever I considered new features I could ask myself, &#8216;could an old cheap LCD toy do this?&#8217;. It really helped me to focus on a straightforward UI and a consistent experience.

I did cheat a bit on the export application. It&#8217;s a separate page with a pretty standard web app UI. But I think of it as something you do on your computer after uploading the data from the toy. I mean people had PCs in the 90s. The even had USB cables toward the end. Maybe there was a cult community around the toy and they made their own applications. I&#8217;m not sure exactly when it started, but I sort of have this whole mythology built up in my head around this thing.

**Too Many Dots**

This was my first real attempt at seeing what Angular.js could do and I learned a lot about what NOT to do with Angular.js. I originally made the main LCD display as a grid of DOM elements with Angular.js directives that applied a class of &#8216;on&#8217; or &#8216;off&#8217; to each pixel based off of data in an array. Long story short, letting Angular handle the state of 512 individual pixel elements was much slower than I had hoped for, so I switched to using HTML canvas for drawing instead. It&#8217;s a bit of a shame because if I could have kept it like that, it would have been super easy to add some CSS transitions to simulate a slow pixel response time as the pixels faded from on to off.

**Not Enough Frames**

Since everything in Super Micro Paint is done on the client side, and I didn&#8217;t want to host any data, I included a feature to push gifs to an external image host so people share could share their creations more easily. I wanted to pick an external service that did video conversion so users could share to sites that don&#8217;t like raw gifs, like Twitter.

Originally, I used gfycat. But at the last minute I discovered that their video conversions sometimes had wonky looping when playing back in Chrome. The video would skip over the last frame very quickly before looping. It looked bad. One frame missed is a big deal when you only have four frames. I tried tweaking the speed of the gif, and finally got something that worked in Chrome, but that version had a problem in other browsers instead. I don&#8217;t know if you need special encoding settings to make a four frame video that loops smoothly in all browsers, but I guess it must be a tricky edge case. Anyway, I tried imgur and their video conversions seemed to loop correctly. So I switched to imgur, which has been working fine so far.

**Links**

  * [Super Micro Paint][1]
  * [Super Micro Paint source at Github][2]
  * [Super Micro Paint official Twitter account][3]
  * [Metafilter thread][4]
  * [Metafilter Projects thread][5]
  * [Metafilter Podcast mention][6] (around 28:30)
  * [Super Micro Paint mlkshk group][7] (Logged in [mlkshk][8] members only, sorry)
  * [Super Micro Paint mlkshk RSS feed][9] (Don&#8217;t need to login, but it&#8217;s RSS)

 [1]: https://walsh9.github.io/super-micro-paint/
 [2]: https://github.com/walsh9/super-micro-paint/
 [3]: https://twitter.com/supermicropaint/
 [4]: https://www.metafilter.com/149806/Super-Micro-Paint-Super-Macro-Fun-
 [5]: https://projects.metafilter.com/4615/Super-Micro-Paint
 [6]: https://metatalk.metafilter.com/23718/105-Have-Fun-At-Space-Camp
 [7]: http://mlkshk.com/supermicropaint
 [8]: http://mlkshk.com/
 [9]: http://mlkshk.com/shake/supermicropaint/rss