---
layout: post
title:  "Games should have optimise for streaming option"
date:   2023-02-26 16:30:00 +0200
categories: Games streaming mtg arena entropy video compression lossy
---
# Games should have "optimise for streaming" option

If you have watched streamed gameplay during your lifetime, you might have noticed many video compression related [artifacts](https://en.wikipedia.org/wiki/Compression_artifact) in those streams. Some of those artifacts are more annoying than the others, and inconvenience varies, but the situation could be greatly improved if developers added *"optimise for streaming"* option to their games.

## Magic: The Gathering Arena - the example

**Magic: The Gathering Arena** is a free-to-play digital collectible card game developed and published by **Wizards of the Coast**. It is available for PC, Mac and mobile platforms. It is a turn based game where every card has art, text and maybe some visual effects when card does something (enters the battlefied, uses ability etc.).

![Mtg arena battlefield]({{ site.url }}/images/mtg_effects_small.jpg "Mtg arena battlefield")  

Above is a small screenshot of the gameplay. There are different visual battlefields in the game, the one shown in screenshot is IMHO the worst offender. 

### Issue 1, noise effects

For lossy video compression, the worst thing you can usually do, is to add some noise ([entropy](https://en.wikipedia.org/wiki/Entropy)) to the image. Or to be more precise, add dynamic (temporal) noise, so in every frame the noise is not same as it was on previous frame. If you don't believe me, watch [Why Snow and Confetti Ruin YouTube Video Quality](https://www.youtube.com/watch?v=r6Rp-uo6HmI) by **Tom Scott**.

The battlefield in this case has multiple different noise effects. For image quality, the most problematic ones are the rain and the fog.

![Mtg arena rain]({{ site.url }}/images/mtg_arena_rain_bad.png "Mtg arena rain")  
(4 x zoom, you might notice the two long vertical lines)  

![Mtg arena battlefield]({{ site.url }}/images/mtg_arena_fog_bad.png "Mtg arena fog")  
(3 x zoom, you might notice the color changes over the bottom gray part)  

In still shots you cannot see it, but they move and they animate. So when you watch gameplay e.g. in YouTube, you will see something like

![Mtg arena rain streamed]({{ site.url }}/images/mtg_arena_rain_bad_2.png "Mtg arena rain streamed")  
(3 x zoom, you might notice the rain drops cannot be seen)  

![Mtg arena battlefield streamed]({{ site.url }}/images/mtg_arena_fog_bad_2.png "Mtg arena fog streamed")  
(3 x zoom, you might notice the fog effect is gone)  

So as you can see, the video encoder cannot properly handle the rain and the fog, but it still tries, because they are part of the image. This trying also steals bitrate from more useful parts of the gameplay. The rain and the fog don't have any gameplay related reasons, they are just visual effects. So why can't we remove them when we are streaming the gameplay?

### Issue 2, effects going over the text

If you don't play MTG 24/7, you won't remember what each card does. But you can move the cursor to the card, and game will tell you what the card does. But if you are watching a stream, then you cannot move your own cursor, and because of that, it is quite important that the visual effects won't hide any texts. Unfortunately that is very common.

![Mtg arena card effect streamed]({{ site.url }}/images/mtg_arena_read_card_bad.jpg "Mtg arena card effect streamed")  

I don't even know why effects are drawn over the text, but there must be some reason.

### Issue 3, font legibility and readability

Most game engines don't have top of the line font rendering capabilities when it comes to legibility and readability. And usually teams choose fonts that more stylish than functional. But for streaming purposes even small improvements could be really useful, like it might be better to a have bit bigger font size and maybe even use different font. Or add solid color backgrounds for certain texts. 

For Arena, one of the issues is that cards that are on the battlefield use rotation when they are [tapped](https://mtg.fandom.com/wiki/Tap). And that makes the default font a bit hard to read. 

![Mtg arena card font rotate]({{ site.url }}/images/mtg_arena_read_bad.png "Mtg arena card font rotate")  

## How to improve

Easy thing to do is to open any game streaming service, find videos of your game and see if there is anything that could be done to make it better for viewers. If you want to automate things, then you can e.g. measure [PSNR](https://en.wikipedia.org/wiki/Peak_signal-to-noise_ratio) or [SSIM](https://en.wikipedia.org/wiki/Structural_similarity) by capturing two videos at the same time (one with lossless compression and another one with common streaming quality lossy compression) and create regression tests for this.

You can help video compression process with e.g. using solid colors in certain UI elements (no fancy textures), blurring non useful elements / areas, adjusting animations (or removing them completely), disabling particles (or reducing amount of particles), disabling shadows and maybe even using different assets when streaming is happening.

Also avoid color [red](https://graphicdesign.stackexchange.com/questions/21204/why-do-jpeg-files-blur-red-more-than-other-colors).

## How to be great

Most lossy image and video codecs operate on pixel blocks (e.g. 4x4, 8x8). If you properly align e.g. your gameplay or UI elements to be in certain places, you can improve their compression quality. 

You could also use entropy budget for scenes / assets to make sure *streamability* (remember, I coined it) stays good all the time.