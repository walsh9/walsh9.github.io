---
title: "asciibots.js"
home: https://walsh9.github.io/asciibots/
sortorder: 4
links:
  - title: "Source"
    url: https://github.com/walsh9/asciibots
  - title: "Blog Post"
    url: https://walsh9.net/projects/asciibots-js/
---
<pre style="display:inline-block" class="bot"></pre>
<pre style="display:inline-block" class="bot"></pre>
<pre style="display:inline-block" class="bot"></pre>
<script src="../js/asciibots.min.js"></script>
<script>
(function(){
    var bots = document.querySelectorAll('.bot');
    for(var i = 0; i < bots.length; i++) {
        bots[i].textContent = Asciibots.bot();
    }
    setInterval(function() { 
        for(var i = 0; i < bots.length; i++) {
            if (Math.random() < 0.25) {
                bots[i].textContent = Asciibots.bot();
            }
        }
    },
    Math.random() * 1000 + 800);
}());
</script>

A Javascript library and jQuery plugin for generating little randomized ASCII art robots.
