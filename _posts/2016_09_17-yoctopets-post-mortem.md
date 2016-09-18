# yoctoPets Post-mortem

I recently made a weird virtual pet simulation called [yoctoPets](http://js13kgames.com/entries/yoctopets) for the [js13kgames](http://2016.js13kgames.com/) competition. The theme this year was 'Glitch'. Hera are a few things I learned while making this game.

## Naive simulation can have surprisingly good results.
When I wanted to add a dot-matrix style printer effect, I did some quick Googling to check out how exactly did they work, and particularly what flaws gave dot-matrix printouts their distinctive look. Well, as the name 'dot-matrix' suggests, they print everything out as a grid of dots. One thing that really stuck out was the fact that the alignment of dots from row to row was subject to analog imperfections.

So to simulate this I took a very straightforward approach and just drew each square yoctoPet pixel as a 4x4 grid of round dots, offsetting the horizontal position of each dot by a tiny random amount to create imperfections. I originally assumed I might have to do more work and this would be a first step, but when I saw the result it just looked great.Okay, I did do a little more work to make the realtime printing effect, but again that was simply drawing the dots row by row and moving the paper just like a real printer would do. And making the ink run out was just a matter of increasing transparency by a tiny amount for each dot printed. Basically I just tried what was obvious instead of looking for clever tricks.

![screenshot of printer results](i/yoctopets_printer.png)

In the game, a small melody plays when your pet dies. I guess it shouldn't be surprising, but I was quite pleased that all I had to do was copy the frequencies and durations of the notes off some sheet music and beep them out over the Web Audio API and it sounded like music.

![sheet music for 'shave and a haircut'](i/Shave_and_a_Haircut_in_C.png)

=> 

```javascript
var C4 = 263;
var B3 = 247;
var A3 = 220;
var G3 = 196;
var REST = 0;
var SHAVE_AND_A_HAIRCUT = [
  {frequency: C4, duration: 1/4},
  {frequency: G3, duration: 1/8},
  {frequency: G3, duration: 1/8},
  {frequency: A3, duration: 1/4},
  {frequency: G3, duration: 1/4},
  {frequency: REST, duration: 1/4},
  {frequency: B3, duration: 1/4},
  {frequency: C4, duration: 1/4},
];
```

=>

<p data-height="196" data-theme-id="0" data-slug-hash="KgrYwB" data-default-tab="js,result" data-user="walsh9" data-embed-version="2" class="codepen">See the Pen <a href="http://codepen.io/walsh9/pen/KgrYwB/">shave and a haircut</a> by Matt Walsh (<a href="http://codepen.io/walsh9">@walsh9</a>) on <a href="http://codepen.io">CodePen</a>.</p>
<script async src="//assets.codepen.io/assets/embed/ei.js"></script>

## Bitmap fonts are easy
Had to do a tiny font for the pixel screen and displaying it wasn't much more work than drawing any other tile. Just have to map pixel positions in the graphic to an array of letters instead of using tile indices or tile names.

![yoctopets pixel font](i/yoctopets_font.png)

=>

![screenshot of font in action](i/yoctopets_text.png)

## Google Closure Compiler really is a compiler

I always just thought of it as a fancy minifier.  But when you turn on those advanced optimization features it starts to get really particular about your code really fast.  I didn't have a lot of time and was never that close to the 13k limit, so I didn't get into it too much, just doing the minimal amount of source code annotation to keep Closure Compiler happy.  But it did get me thinking about the possibilities of using it in other projects. Seems good when you want sanity checks on your code beyond what a linter can provide.

## As always, CSS gradients and shadows are fantastic
Just look at those buttons. Look at that paper.

![screenshot showing off shiny case and crisp paper](i/yoctopets_paper.png)

There's more but I don't want to reveal all of the mysteries. Please [check out the game](http://js13kgames.com/entries/yoctopets) and adopt your own yoctoPet today.
