---
layout: post
title:  "Reducing overdraw, tip #3"
date:   2017-05-28 17:05:00 +0200
categories: overdraw texture reduce tip accurate
---
# Reducing overdraw, tip #3

As usual, this post is simple and short. I give one example that developers/artists can use to reduce [overdraw](https://en.wikipedia.org/wiki/Fillrate) in their app/website/game.

&nbsp;

## Use accurate geometry instead of one basic triangle/quad

On earlier posts ([1]({{ site.baseurl }}{% post_url 2017-02-04-reducing-overdraw-01 %}) and [2]({{ site.baseurl }}{% post_url 2017-05-27-reducing-overdraw-02 %})) I have focused on UV adjustments. This time the tip is to adjust drawing geometry in such way that it matches better with texture.

While basic geometry is easier to understand and organize, using more accurate (accurate in this context means that there is no polygon area for completely transparent pixels) geometry for a texture can reduce overdraw operations significantly. This usually requires custom mesh and UV coordinates, so some additional work is required.

You don't have to be pixel accurate in your geometry, and you can even use some [tools](knowledge.autodesk.com/support/maya-lt/learn-explore/caas/CloudHelp/cloudhelp/2015/ENU/MayaLT/files/Polygon-selection-and-creation-Convert-textures-to-a-polygon-mesh-htm.html) to speed up the process for generating needed meshes for your textures.

In best case scenario you might even be able to reduce number of transparent pixels to zero with this method, if texture alpha is on/off type. That way you can completely eliminate transparency and speed up rendering.

Since accurate geometry usually involves more triangles, the GPU will get a bit more work in vertex department, but nowadays few additional vertex operations are better option than overdrawing thousands of pixels.

&nbsp;

## Static sample

![Comparison with normal and accurate geometry]({{ site.url }}/images/accurate_geometry_01.png)

(instead of one quad we render five triangles)

&nbsp;

## Live sample

You can find WebGL sample made with [Babylon.js](http://www.babylonjs.com) from [here]({{ site.url }}/demos/babylon-js/babylon-js_avoid_overdraw_example_03.html)