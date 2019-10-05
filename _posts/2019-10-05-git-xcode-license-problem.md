---
layout: post
title:  "Xcode update can break your build automation"
date:   2019-10-05 12:00:00 +0200
categories: mac xcode git license
---
With **Mac OS** the proper way to update applications is via App Store. If you install **Xcode** you will get some common development tools like **git** to your system.

Unfortunately updating the Xcode via the App store can also break your local build automation as can be seen in image below

![Git xcode license]({{ site.url }}/images/xcode_git_license.png)

Problem is that App store update process doesn't actually start Xcode at all. And one has to accept *Xcode/iOS license* before one can use ANY tools that come with Xcode, even if those tools are shared under [Open Source Licenses](https://opensource.org/licenses). So if you just update Xcode but do not start it, the license hasn't been accepted and those tools just print out text that might or might not break your build automation.

So every time you update Xcode via App store, remember to start Xcode and accept the license agreement. 