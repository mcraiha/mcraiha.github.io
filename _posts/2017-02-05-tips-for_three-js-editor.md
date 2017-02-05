---
layout: post
title:  "Tips for Three.js editor"
date:   2017-02-05 14:50:00 +0200
categories: tips three.js editor
---
# Three.js editor

If you don't know what [Three.js](https://threejs.org/) is, then here is a quote from [Wikipedia](https://en.wikipedia.org/wiki/Three.js) *"Three.js is a cross-browser JavaScript library/API used to create and display animated 3D computer graphics in a web browser. Three.js uses WebGL."*

Most people don't know that there is a [build-in editor](https://threejs.org/editor/) in Three.js that can be used to e.g. create visual demos and games.

I have collected some tips to this post that will hopefully help people with Three.js editor

There is also a lovely [Hacker News discussion](https://news.ycombinator.com/item?id=13299479) about Three.js editor

And if you want to see some sample demos made with Three.js editor then check out [mrdoob.neocities.org](https://mrdoob.neocities.org/)

## Tip 01: Start from scratch

Just select **File -> New**

![Start from scratch]({{ site.url }}/images/three-js_tip_01.png)

&nbsp;

## Tip 02: Add a cube/box

Just select **Add -> Box**

![Add a cube/box]({{ site.url }}/images/three-js_tip_02.png)

&nbsp;

## Tip 03: Rename an object

1. Select **SCENE** panel
2. Select **an object** you want to rename
3. Write wanted name to **Name** field and press Enter

![Rename an object]({{ site.url }}/images/three-js_tip_03.png)

&nbsp;

## Tip 04: Make object rotate in Play mode

This is first not so trivial tip.

1. Add a box to scene (**Add -> Box**)
2. Select the box and from **SCENE** panel select **OBJECT** panel and press **NEW** button under **SCRIPT**
3. Type in some name for script and press **EDIT** button
4. Copy and paste following code into code editor, then close the code editor with X.

```javascript
function update( event ) 
{
	this.rotation.z += 0.1;
}
```

5. Press play, and see how the box rotates

![New script]({{ site.url }}/images/three-js_tip_04a.png)
![Script name and edit]({{ site.url }}/images/three-js_tip_04b.png)
![Paste rotation code]({{ site.url }}/images/three-js_tip_04c.png)

&nbsp;
