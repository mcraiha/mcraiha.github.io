---
layout: post
title:  "Cheapo Katex linked list"
date:   2026-02-14 11:00:00 +0200
categories: Katex Latex linked list
---
# Cheapo Katex linked list

Sometimes you have to use [Katex](https://katex.org/) to show formulas in your presentation/webpage. And sometimes you have to go a bit deeper, and show [a linked list](https://en.wikipedia.org/wiki/Linked_list) with Katex. There might be a *"correct"* way to do that, but I just wanted a quick solution for the problem.

```latex
\boxed{ \hspace{0.1em} 12｜\bullet \>}\hspace{-0.5em}— \hspace{-0.5em}\longrightarrow \hspace{-0.3em} \boxed{ \hspace{0.1em} 88｜\bullet \>}\hspace{-0.5em}— \hspace{-0.5em}\longrightarrow \hspace{-0.3em}\boxed{\mathrm{X}}
```

it should output something like

![Linked list]({{ site.url }}/images/katex_linked_list.png)

you can replace the `12` and `88` with the values you want/need.