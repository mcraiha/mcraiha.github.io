---
layout: post
title:  "Simple Babylon.js pixel / fragment shader"
date:   2017-04-23 10:55:00 +0200
categories: simple Babylon.js pixel fragment shader webgl
---
I have tested out both [Three.js](https://threejs.org) and [Babylon.js](http://www.babylonjs.com) for generating simple [WebGL](https://en.wikipedia.org/wiki/WebGL) scenes. So it is time to share some Babylon.js related examples.

## Simple pixel shader

When I want simple shader, I do not mean one color dot. I usually want both UV coordinates + some kind of time to be feeded to the shaders.

Following image is a still picture from running shader that animates noise with pixel / fragment shader
![Shader still]({{ site.url }}/images/pixel_shader_noise_babylon-js.jpg)

And you can [test out]({{ site.url }}/demos/babylon-js/babylon-js_basic_pixel_shader.html) the scene in your browser, but it seems it does not render correctly with mobile devices.

### Notes

* Vertex shader is defined in **vertexShaderCode** and it does not do anything special, it just forwards the UV coordinates to Pixel shader
* Pixel shader is defined in **fragmentShaderCode**. It has a *float rand(float n)* function for generating not so random floating point values. Also Pixel shader takes **time** as a input, and it is used to animate the noise.
* Babylon.js scene creation part just adds a camera, creates the shadermaterial, creates a cube/box, joins the shadermaterial to cube/box and makes an animation function that increases **time** before scene is rendered

Using separate script sections for shaders is not the only way to do this. You can also use separate files for shaders or something that is called **BABYLON.Effect.ShadersStore**. If you want more info about this then check out [Shader Material](http://babylonjsguide.github.io/advanced/Shader_Material) part from Babylon.js guide. 

### Source code

Below is full source code for the sample. You need working internet connection for testing since scripts **hand.minified-1.2.js** and **babylon.js** live in **babylonjs.com**

<script src="https://gist.github.com/mcraiha/cae12c3bb8ea7d02e0cb31f8e01a16bd.js"></script>