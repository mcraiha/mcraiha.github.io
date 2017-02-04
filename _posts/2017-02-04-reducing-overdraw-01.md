---
layout: post
title:  "Reducing overdraw, tip #1"
date:   2017-02-04 17:10:00 +0200
categories: overdraw texture reduce tip trim crop
---
# Reducing overdraw, tip #1

This post is simple and short. I give one example that developers/artist can use to reduce [overdraw](https://en.wikipedia.org/wiki/Fillrate) in their app/website/game.

&nbsp;

## Trim completely transparent pixels from sides

This is something that shows up quite often. Artist/designer has chosen certain resolution for an image element, but only uses part of the 2D texture area and rest of it is filled with completely transparent pixels. Then game engine/app/web browser just [blits](https://en.wikipedia.org/wiki/Bit_blit) the whole texture to the screen and unnecessary overdraw happens. 

So tip is that you [trim/crop](https://en.wikipedia.org/wiki/Cropping_(image)) the completely transparent pixels out of the image. This might require new UV coordinates and/or new pivot point (so if needed, consult your local programmer before doing this), but if there are lots of transparent pixels, it is well worth it.

&nbsp;

## Static sample

![Comparison with normal and trimmed]({{ site.url }}/images/side_trim_withshow.png)
(on the left side is the original 256x256 texture (65536 pixels), on the right side is new 157x157 texture (24649 pixels) and that means new texture will reduce over 40000 overdraw operations)

&nbsp;

## Live sample

