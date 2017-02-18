---
layout: post
title:  "Better compression Vol. 02"
date:   2017-02-18 19:40:00 +0200
categories: compression png jpg entropy reduction blur colors
---
This is a second part of series that gives some guidance for getting better compression results when handling images or videos

There are many tips and tricks that can be used to get better compression when handling images or videos. With better compression I mean in this context that one can get similar (or near similar) image quality, but use less bits (storage space) for it.

Warning, this post contains lots of image data!

&nbsp;

## Reduce entropy

This posts uses **entropy reduction** as one of those bit saving optimizations. 

Entropy in this context means a measure of the "disorder" of a system. Since most compression schemes are allergic to randomness, one can improve compression by making content to have less entropy.

&nbsp;

### Gist
You can do all kinds of entropy reduction tricks for an image before compression and get better compression results.

&nbsp;

### Proofs

Examples use [statue photo](http://creativevix.com/images/mainstock/151.jpg) that I have resized to 480x320 resolution before doing any other processing.

First the PNG versions ([lossless compression](https://en.wikipedia.org/wiki/Lossless_compression) chain)

| Description | Image |
|:-------------:|:-------------:|
| **Original** (333 121 bytes) | ![Original]({{ site.url }}/images/151_original.png) |
| **Partial blur** (316 408 bytes) | ![Partial blur]({{ site.url }}/images/151_blurred.png) |
| **Reduced colors** with [dithering](https://en.wikipedia.org/wiki/Dither) (98 017 bytes) | ![Reduced colors with dithering]({{ site.url }}/images/151_reduced_colors.png) |
| **Reduced colors** no dithering (89 786 bytes) | ![Reduced colors, no dithering]({{ site.url }}/images/151_reduced_colors_nodithering.png) |

&nbsp;

Then the JPG versions, quality 90 ([lossy compression](https://en.wikipedia.org/wiki/Lossy_compression) chain)

| Description | Image |
|:-------------:|:-------------:|
| **Original** (41 426 bytes) | ![Original]({{ site.url }}/images/151_original.jpg) |
| **Partial blur** (34 257 bytes) | ![Partial blur]({{ site.url }}/images/151_blurred.jpg) |
| **Reduced colors** with [dithering](https://en.wikipedia.org/wiki/Dither) (42 815 bytes) | ![Reduced colors with dithering]({{ site.url }}/images/151_reduced_colors.jpg) |
| **Reduced colors** no dithering (42 363 bytes) | ![Reduced colors, no dithering]({{ site.url }}/images/151_reduced_colors_nodithering.jpg) |

&nbsp;

As you can see from above tables, the entropy reduction tricks have different kind of results based on compression method. Color reduction (from 24 bit colors to 8 bit colors) with dithering works wonderfully with lossless compression, but with lossy compression it just increases file size.


### How can I apply these to my project
Most image editors and video editing tools offer easy shortcuts that one can use to blur images/videos.
![Blur image in Paint.net]({{ site.url }}/images/paint_net_blur.png)

Usually there are multiple blur options, and you should test them out to get the visual output you want. More blur usually means better compression.

Good target for partial blur filter are parts that have high amount of noise. 

You can also manage blur during shooting/recording by [focusing subjects](http://www.digital-photo-secrets.com/tip/2210/understanding-focus/) in certain way. If your targets don't move much during shooting/recording, you can pretest your gear and find good settings that you can use.

Color reduction is a common option in image editors but in many video editing tools it does not exist. Some programs allow you to select different dithering methods when doing color reduction, and they give different visual outputs, so test them out.

&nbsp;

### Why it works
Less noise means less entropy and therefore better compression. Blur reduces noise and also lessens the contrast which helps lossy compression methods since there will be less high frequency components in the image.

Color reduction (with dithering) works best with lossless compression since smaller color space is easier to compress. Dithering usually increases entropy but since the colorspace is reduced, entropy increase is usually minimal when color space stays reasonable. 
&nbsp;

