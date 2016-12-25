---
layout: post
title:  "Simple markdown to html in GitHub!"
date:   2016-12-06 18:00:00 +0200
categories: jekyll GitHub
---
When internet was a new thing to me, I loved [HTML](https://en.wikipedia.org/wiki/HTML) because with it I could easily create some content for the web. Nowadays I hate it, I don't want to mess with CSS and/or Javascript to create web pages that someone could read. [Markdown](https://en.wikipedia.org/wiki/Markdown) is much better option, but is quite hard to get readable HTML rendering for browser from plain markdown.

Only option for me at this point is to use De facto standard of static web page generation tools, and that monster has a name, and it is **[Jekyll](https://jekyllrb.com)**.

It took me over 3 hours to get Jekyll to run on [Bash on Ubuntu on Windows](https://msdn.microsoft.com/en-us/commandline/wsl/about). Mainly because **apt-get** provides us **Ruby** 1.9 and newer versions of Jekyll want newer. At one point I was wondering if there is cloud service for Jekyll, and I coined a phrase **#jekyllaas**.

I would gladly pay for Jekyll like system that would be build without dependencies and could be run in browser/cloud. But AFAIK something like that doesn't exist yet.

As you might know, [GitHub pages](https://pages.github.com/) supports Jekyll, ~~but that support is [very limited](https://help.github.com/articles/configuring-jekyll/), since only safe mode can be used and only supported theme is [Minima](https://github.com/jekyll/minima)~~.
(**UPDATE 25.12.2016:** GitHub [has improved](https://github.com/blog/2295-new-theme-chooser-for-github-pages) the Jekyll support and now there are [13 themes](https://pages.github.com/themes/) supported)

I could build static pages via local Jekyll if I wanted better customization options but since it is too cumbersome, I want to use plain GitHub method (which is using **git** for **.md** files). 

I luckily found out [nice basic tutorial](https://github.com/henrythemes/hello-minima-theme) for using Minima in GitHub. Simple and effective.

But there are some useful tricks you can do with [Liquid](http://shopify.github.io/liquid/) template language. And since I have to add [Front Matter](http://jekyllrb.com/docs/frontmatter/) to these markdown files, I won't get the pure markdown experience I would want, but I can still dream about it... 
