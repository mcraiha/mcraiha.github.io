---
layout: post
title:  "App Tracking Transparency review process lottery"
date:   2021-05-10 18:00:00 +0200
categories: apple review Tracking Transparency
---
# App Tracking Transparency review process lottery

Two weeks ago **Apple** released the **iOS 14.5** and also started to do more careful review process for iOS apps. That is because they want to be sure that apps available in **App Store** follow their [App Tracking Transparency](https://developer.apple.com/app-store/user-privacy-and-data-use/) (ATT) guidelines. Unfortunately for developers the process is a lottery draw.

## Example 1. Star Wars: Galaxy of Heroes

**Star Wars: Galaxy of Heroes** is a game made by **Capital Games** and published by **Electronic Arts** (EA). They use very direct App Tracking Transparency prompt as soon as the game starts, that tells users game's third party logins (basically **Facebook** login) won't work if you opt out from tracking.

![Galaxy of Heroes ATT]({{ site.url }}/images/att_heroes.jpg)  

So we figured out that since EA is a big figure in gaming markets, we should be able to follow their lead. We also showed the prompt when the game starts and we used almost the same text as Galaxy of Heroes to be sure that we won't cause issues in review process. Naturally we were wrong. We got rejected immediately with complain that said something like *"you should not force or manipulate users into enabling tracking"*.

If you run big enough company, it seems that you won't get very strict App Store review process. But if you are a smaller developer, then the process will hit you in the head.

Luckily there are other big name game companies left, so our next example comes from **Supercell**.

## Example 2. Brawl Stars

**Brawl Stars** is a game made and published by **Supercell**. They only show App Tracking Transparency prompt when you try to use Facebook login first time. If you opt out from tracking, the Facebook login won't work (and you cannot make it work anymore unless you delete the app and install it again). That seems somewhat reasonable. So we tried exactly same approach (we even copied the ATT text from Brawl Stars (minus the Super Cell ID part) to follow their example).

![Brawl Stars ATT]({{ site.url }}/images/att_brawl_stars.jpg)  

As you can guess, Apple rejected that also. This time Apple said that developers cannot disable features if player opts out from tracking. Again, a lottery.

## More examples

If you want to see a gallery of these prompts then head to [attprompts.com](https://www.attprompts.com/), and you can easily see that there is a high variance between accepted titles. Some want to access your device, some want to provide you a better ad experience and some want to reach you.

## Maybe avoid ATT?

Someone might say to us, do not use ATT and problem is solved. Unfortunately that wouldn't work, the first rejection we got from Apple is because ATT was missing. So we added ATT and have already got two rejections. Our game does not show ads if that is what you are wondering.

