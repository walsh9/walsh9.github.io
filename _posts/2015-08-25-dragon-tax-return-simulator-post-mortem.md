---
title: Dragon Tax Return Simulator 2015 - Post Mortem
author: walsh9
layout: post
categories:
  - projects
  - games
---
[Dragon Tax Return Simulator 2015](http://ludumdare.com/compo/ludum-dare-33/?action=preview&amp;uid=56320) is my first Ludum Dare entry. Once the theme was announced I brainstormed a list of about a dozen ideas, and then narrowed them down based on whether they were 1. doable, 2. interesting. Somehow this dragon tax game idea came out on top. While I was originally trying for a compo entry, when I realized I wasn't finishing on day 2, I adjusted trajectory toward the jam.

**Tools**

Javascript - This is a mostly from scratch (libraries used below) HTML5 game. So if it looks bad or doesn't work for you then I probably didn't test in your browser/os.

Google Fonts - A great resource and allowed me to take full advantage of the "Fonts are allowed." exception. I doubt I'd have even tried this idea if I didn't know about Google Fonts.

Handlebars.js - I'd never used it before but it was great for making templates for all the various forms that got created.

jQuery - jQueryUI made it super simple to make all the paper draggable.

**The Good**

I feel like I really got a lot of value out of simple randomization.

The instructions use random values for most of the 'rules' so you can't just learn the tax code.

The random name generator was really fun to make even though all it does is stick some random syllables together (about half the time it just picks a 'normal' firstname from a list). I decided this was not the time to try and figure out markov chains or anything fancy like that. I think this simple randomizer still came out fine.

![Names](/i/names2-550x83.png)

I'm also happy with how well the random note generation worked out with its simple templates.

For example here's the farmer complaint template (with the HTML stripped out):

```javascript
{% raw %}
Hey {{dragonEpithet}}!

{{exasperatedComplaint}}
You burnt up {{value}} gold worth of my crops!
{{farmerAppeal}}
{{peasantNotice}}
{{partingShot}}

{{randomName}}, {{location}}

P.S. {{grovelling}}
{% endraw %}
```

And the results:

![farmer complaint note](/i/complaint.png)

It was fun to write all the sentences that filled these templates, but I still want to add more since the notes can still get repetitive.

**The Bad**

Originally, the 'time limit' in the game was only going to be 5 minutes. On the second day I actually tried a test run. One thing I noticed was that 5 minutes was *nowhere near enough* time. I used that discovery as an opportunity to cut extra forms, simplify the main form, and increase the time limit to 10 minutes. I probably could have saved myself a lot of time if I'd tried playing the game earlier.

Also, I probably shouldn't have waited until the third day to add all the logic that makes it "a game". I mean stuff like the dialogs, finish state, endgame report, etc. I was kind of pushing my luck as I rushed to get those all in before the deadline.

**Ideas That Didn't Make It**

I wanted to add more graphics. Just things like little official seals/stamps for some of the paperwork. Burnt edges on the papers. A little pixel art dragon claw cursor.

And I wanted some of the complaints from shopkeepers to be on shop letterheads with randomized shop names but I was running out of time and ended up just reusing the design from the peasant notes.

([Originally posted here](http://ludumdare.com/compo/2015/08/25/dragon-tax-return-simulator-2015-post-mortem/))
