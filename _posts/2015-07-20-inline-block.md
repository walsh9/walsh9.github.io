---
layout: post
title:  "Inline, Block, and Inline-block"
date:   2015-07-20 09:00:00
categories: "programming"
---

When writing HTML, each element you put on the page stakes out it's own little rectangle of space. Each element also has a special property called `display`. The `display` property sets rules for how those little rectangles behave.

Two of the most common values for `display` are `block` and `inline`. So what's the difference?

## Block

Block-level elements are very protective of their personal space. They won't let any other elements share a row with them. They want their own line. They move down to a new row and stake out all the space to the left and right of them, and will even push any following elements down to the next row. Divs like to stack up vertically.

Some examples of elements that are block-level by default: `<div>`, `<p>`, and `<h1>`.

## Inline

Inline elements like to go with the flow. They work a lot like text. They'll sit next to other inline elements on the same row, and depending on their contents they even wrap around lines. Just a train of rectangles going horizontally across the screen line by line.

But inline elements are pushovers. They don't like to take up more space than they need to. You can't set a width or height on inline elements. And you can't adjust top or bottom borders or padding.

Some examples of elements that are inline by default: `<span>`, `<strong>`, and `<a>`.

## Inline-block

Inline-block is a special hybrid type of rectangle. It flows like an inline element, but doesn't have any of the sizing, margin, or padding restrictions.

## A note about positioning

Using floats, fixed positioning, or absolute positioning can affect the layout in ways that seem to override some of the above rules. These positioning methods take the element out of the main page flow, which is one layout universe, and create their own parallel layout universes. It's a bit much to go into depth here, but the layout rules about block elements taking the whole row are only guaranteed for static positioned elements.