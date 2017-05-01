---
layout: post
title:  "Simple Babylon.js vertex shader"
date:   2017-05-01 21:55:00 +0200
categories: simple Babylon.js vertex shader webgl
---
I have tested out both [Three.js](https://threejs.org) and [Babylon.js](http://www.babylonjs.com) for generating simple [WebGL](https://en.wikipedia.org/wiki/WebGL) scenes. So it is time to share some Babylon.js related examples.

## Simple vertex shader

Previously I made [a simple pixel shader example]({{ site.baseurl }}{% post_url 2017-04-23-simple-babylon-js-pixel-shader %}) and this time I will focus to simple vertex shader example.

I won't be posting a full HTML example this time since I want to show you how nice [Babylon.js Playground](https://www.babylonjs-playground.com) is for sharing simple WebGL scenes.

Babylon.js Playground allows people to edit, share and execute their Babylon.js related *var createScene = function()* parts in browsers. You can find code of this blog post from [http://www.babylonjs-playground.com/#1OH09K#6](http://www.babylonjs-playground.com/#1OH09K#6) and you can modify it (if you want) and test it out directly from your browser.

Via Babylon.js Playground people can also download projects directly to .zip file in case they need more editing powers (e.g. add Javascript controls) or have to publish scenes in certain websites.

Following image is a still picture from running shader that does wave effect with vertex shader
![Shader still]({{ site.url }}/images/vertex_shader_wave_babylon-js.jpg)

If you want to see this example outside of Babylon.js then open [following link]({{ site.url }}/demos/babylon-js/babylon-js_basic_vertex_shader.html)

### Notes

* Vertex shader is defined in **BABYLON.Effect.ShadersStore["customVertexShader"]=** and it alters both X and Y coordinates of every vertex it receives. UV coordinates are forwarded to Pixel shader
* Pixel shader is defined in **BABYLON.Effect.ShadersStore["customFragmentShader"]=**. It just reads correct pixel from texture.

### Source code

<script src="https://gist.github.com/mcraiha/af957be2628efeb7eb67a1084e9a3f01.js"></script>