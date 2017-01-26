---
layout: post
title:  "Better compression Vol. 01"
date:   2017-01-06 19:30:00 +0200
categories: compression png rotation
---
This is a first part of series that gives some guidance for getting better compression results when handling images or videos

There are many tips and tricks that can be used to get better compression when handling images or videos. With better compression I mean in this context that one can get similar (or near similar) image quality, but use less bits (storage space) for it.

## Rotation

This posts uses **rotation** as one of those bit saving optimizations. 

For those who have never dived into science of [signal processing](https://en.wikipedia.org/wiki/Signal_processing), be ready for surprise.

### Gist
You can rotate (±90 degrees rotation) an image before compression and get better compression results because of the rotation.

### Proof

|      | Original       | 90 degrees rotated |
|---------------|---------------|---------------|
| **Image** | ![Normal black to white fade texture]({{ site.url }}/images/black_to_white_fade.png) | ![90 degrees rotated black to white fade texture]({{ site.url }}/images/black_to_white_fade_90.png) |
| **File size** | 7 993 bytes | 4 803 bytes |

### How can I apply this to my project
Rotating images is quite easy. Most image editors offer easy shortcuts that one can use to rotate images.
![Rotate image in Paint.net]({{ site.url }}/images/paint_net_rotate.png)

Showing the rotated images correctly is bit harder, but if you have full control of the program, you can use some kind of indicator to mark the textures/images that should be rotated when used. e.g. add tag, use special file names, keep list ... And when you load one those textures/images you can rotate it during decoding. If you cannot control decoding (e.g. HTML environment) then you might be able to rotate image when it is showed. 

{% highlight html %}
<!--Rotate image 90 degrees-->
<img src="image_that_needs_rotation.png" style="transform: rotate(90deg);">
{% endhighlight %}

You can also automate the compression step to see if rotation helps with those images you are using. This means that you will create 3 additional versions (90, 180 and 270 degrees of rotation) of the image and see which one has the smallest file size.

### Why it works
Reordering of the pixels (that is what ±90 degrees rotation does) means that pixels (or bytes of data) will arrive to the lossless compression in different order. 

Image shown in proof section will benefit from rotation because all the same colored pixels are in one row. And since PNG does compression row by row it can basically say that every pixel in first row is black (well it is not THAT easy, but you get the point).

For general case the benefits might be very small, but for certain types of images one can easily get files that are 10% smaller.

### What could be better
There could be (there might already be, I am not sure) an image format where compression step checks the rotation benefits automatically and stores the pixels in best possible rotation. And decoder rotates the image automatically based on image header.