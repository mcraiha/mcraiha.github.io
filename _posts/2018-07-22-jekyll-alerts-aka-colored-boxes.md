---
layout: post
title:  "Jekyll alerts aka colored boxes"
date:   2018-07-22 10:15:00 +0200
categories: jekyll alert liquid markdown template
---
As default markdown does not provide colorful elements for blog posts, one might need some outside help.

Luckily [Jekyll](https://jekyllrb.com/) offers some options that can be used. e.g. in [Jekyll Doc](https://github.com/amzn/jekyll-doc-project) these are known as [alerts](https://idratherbewriting.com/documentation-theme-jekyll/mydoc_alerts.html).

Basically you add some .html templates to your **_include** folder and call them with Liquid template language that Jekyll supports

## Note (shameless mutated copy from Jekyll Doc)
### HTML template
```html
<div markdown="span" style="margin-bottom: 10px; margin-top: 10px; overflow: hidden; color: #31708f; background-color: #d9edf7; border-color: #bce8f1; padding: 15px; border: 1px solid transparent; border-radius: 4px;">❕ <b>Note:</b> {{include.content}}</div>
```
you can also see [note.html](https://github.com/mcraiha/mcraiha.github.io/blob/master/_includes/note.html)
### How to use in markdown
<script src="https://gist.github.com/mcraiha/dea006f2519eba94cc01c08884e8733b.js"></script>

### Outcome
It looks something like
{% include note.html content="Nice blue note" %}
