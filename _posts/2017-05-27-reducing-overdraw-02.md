---
layout: post
title:  "Reducing overdraw, tip #2"
date:   2017-05-27 18:55:00 +0200
categories: overdraw texture reduce tip trim overcrop
---
# Reducing overdraw, tip #2

This post is simple and short. I give one example that developers/artists can use to reduce [overdraw](https://en.wikipedia.org/wiki/Fillrate) in their app/website/game.

&nbsp;

## Overcrop pixels from sides

[Last time]({{ site.baseurl }}{% post_url 2017-02-04-reducing-overdraw-01 %}) I showed how you can reduce overdraw by trimming transparent pixels. This time the tip I am giving is quite similar, you just overcrop some pixels that have very small alpha values.

In most cases you should only overcrop pixels that human eye cannot easily spot after rendering is done. This method requires quite bit of artistic eye, so it isn't suitable for every situation. But it can provide nice performance gains, specially with particles.

&nbsp;

## Static sample

![Comparison with normal and overcropped]({{ site.url }}/images/overtrim_withshow.png)

(left side is the original **256x256** texture (65536 pixels), right side is new overtrimmed **125x152** texture (19000 pixels). Regularly trimmed texture would be **152x152** (23104 pixels) so overtrimming saves about 4000 overdraw operations)

&nbsp;

## Live sample

You can find WebGL sample made with [Babylon.js](http://www.babylonjs.com) from [here]({{ site.url }}/demos/babylon-js/babylon-js_avoid_overdraw_example_02.html)