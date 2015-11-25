---
title: asciibots.js
author: walsh9
layout: post
categories:
  - projects
---
Before we had Game Boys, my cousin and I had a collection of [Tomy Pocket Games][1]. There was [Copter Fight][2], [Caterpillar][3], [Pass The Puck][4], [the race car one][5], and more. They were simple but fun, and they kept us busy and out of my parents' and grandparents' hair on long car trips.

One that I really enjoyed was called [Robot Factory][6]. It wasn't even really a game, just a little slot machine that had different robot heads and parts. You were supposed to get the parts that "matched" for the most points, but lots of times I would just spin to see what came up.  

![Robot Factory Tomy Pocket Game](/i/jmrobotfactory.jpg)

Many years later, now grown up, I noticed a blog I followed was running a 1k code contest. The theme was open-ended, but I think maybe I thought the theme was the number 1000. I remembered Robot Factory. If I made 10 robots with 3 parts, there could be 10 x 10 x 10... 1000 possible robots. I could probably squeeze some ASCII art into 1k of code. It was perfect. So, after drawing and redrawing and applying some manual compression and some code to put it all together, I ended up with 1000 bytes of unreadable Javascript that displayed random robots. I had a lot of fun refreshing the page and looking at what came up. It ended up winning the contest for some reason and I got a fancy external hard drive out of it.

<div style="text-align: center;">
  <pre style="display: inline-block;" class="bot"></pre>
  
  <pre style="display: inline-block;" class="bot"></pre>
  
  <pre style="display: inline-block;" class="bot"></pre>
</div>

I was thinking about this project recently. I found the code still on my hard drive and decided to put it into a readable and maintainable format. I couldn't stop messing with it. I added 6 more robots for a total of 16 so they could be addressed with hexadecimal digits because I though maybe they would be fun as little identicon-like avatars or something. And then I decided the faces were too samey so I added two optional digits for changing the eyes and mouth. It's only a few characters but the faces give the robots a lot of their personality so I think it really improved the variety. It's dumb nostalgia, but I made these face decorations optional mostly because I wanted the classic three digit IDs to still work. Anyway, I'll probably keep tinkering with it from time to time but asciibots.js is up on [GitHub][7] now and a [demo site is here][8].

 [1]: http://www.masters.me.uk/pocketeers/completelist-pocketgames.htm
 [2]: http://www.masters.me.uk/pocketeers/Htm-Designs/ratatat.htm
 [3]: http://www.masters.me.uk/pocketeers/Htm-Designs/splashdown.htm
 [4]: http://www.masters.me.uk/pocketeers/Htm-Designs/passthepuck.htm
 [5]: http://www.masters.me.uk/pocketeers/Htm-Designs/grandprix.htm
 [6]: http://www.masters.me.uk/pocketeers/Htm-Designs/flipflopfaces.htm
 [7]: https://github.com/walsh9/asciibots
 [8]: https://walsh9.github.io/asciibots/

 <script src="/js/asciibots.min.js"></script>
 <script>
(function(){
    var bots = document.querySelectorAll('.bot');
    for(var i = 0; i < bots.length; i++) {
        bots[i].textContent = Asciibots.bot();
    }
}());
</script>