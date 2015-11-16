---
title: asciibots.js
author: walsh9
layout: post
permalink: /projects/asciibots-js
categories:
  - projects
---
Before we had Game Boys, my cousin and I had a collection of [Tomy Pocket Games][1]. There was [Copter Fight][2], [Caterpillar][3], [Pass The Puck][4], [the race car one][5], and more. They were simple but fun, and they kept us busy and out of my parents&#8217; and grandparents&#8217; hair on long car trips.

One that I really enjoyed was called [Robot Factory][6]. It wasn&#8217;t even really a game, just a little slot machine that had different robot heads and parts. You were supposed to get the parts that &#8220;matched&#8221; for the most points, but lots of times I would just spin to see what came up.  
<img class="size-full wp-image-46 aligncenter" src="http://walsh9.net/wp-content/uploads/2014/08/jmrobotfactory.jpg" alt="jmrobotfactory" width="204" height="355" />Many years later, now grown up, I noticed a blog I followed was running a 1k code contest. The theme was open-ended, but I think maybe I thought the theme was the number 1000. I remembered Robot Factory. If I made 10 robots with 3 parts, there could be 10 x 10 x 10&#8230; 1000 possible robots. I could probably squeeze some ASCII art into 1k of code. It was perfect. So, after drawing and redrawing and applying some manual compression and some code to put it all together, I ended up with 1000 bytes of unreadable Javascript that displayed random robots. I had a lot of fun refreshing the page and looking at what came up. It ended up winning the contest for some reason and I got a fancy external hard drive out of it.

<div style="text-align: center;">
  <pre style="display: inline-block;" class="bot crayon:false"></pre>
  
  <pre style="display: inline-block;" class="bot crayon:false"></pre>
  
  <pre style="display: inline-block;" class="bot crayon:false"></pre>
</div>

I was thinking about this project recently. I found the code still on my hard drive and decided to put it into a readable and maintainable format. I couldn&#8217;t stop messing with it. I added 6 more robots for a total of 16 so they could be addressed with hexadecimal digits because I though maybe they would be fun as little identicon-like avatars or something. And then I decided the faces were too samey so I added two optional digits for changing the eyes and mouth. It&#8217;s only a few characters but the faces give the robots a lot of their personality so I think it really improved the variety. It&#8217;s dumb nostalgia, but I made these face decorations optional mostly because I wanted the classic three digit IDs to still work. Anyway, I&#8217;ll probably keep tinkering with it from time to time but asciibots.js is up on [GitHub][7] now and a [demo site is here][8].

 [1]: http://www.masters.me.uk/pocketeers/completelist-pocketgames.htm
 [2]: http://www.masters.me.uk/pocketeers/Htm-Designs/ratatat.htm
 [3]: http://www.masters.me.uk/pocketeers/Htm-Designs/splashdown.htm
 [4]: http://www.masters.me.uk/pocketeers/Htm-Designs/passthepuck.htm
 [5]: http://www.masters.me.uk/pocketeers/Htm-Designs/grandprix.htm
 [6]: http://www.masters.me.uk/pocketeers/Htm-Designs/flipflopfaces.htm
 [7]: https://github.com/walsh9/asciibots
 [8]: https://walsh9.github.io/asciibots/