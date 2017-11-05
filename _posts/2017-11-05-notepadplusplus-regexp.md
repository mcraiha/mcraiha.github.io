---
layout: post
title:  "Notepad++ and regexp"
date:   2017-04-23 10:55:00 +0200
categories: notepad++ notepadplusplus regex regexp regular expression
---
Since regular Windows installation is missing lots of handy tools, it is usually easier to use existing GUI tools for certain tasks. This time the combo is [Notepad++](https://notepad-plus-plus.org/) and [regular expression](https://en.wikipedia.org/wiki/Regular_expression).

## Notepad++
Notepad++ is *a free (as in "free speech" and also as in "free beer") source code editor and Notepad replacement that supports several languages*. Basically all Windows devs and power users should have it installed since it is small, fast and supports all kinds of neat tricks.

## Regular expression
Quote from [Wikipedia](https://en.wikipedia.org/wiki/Regular_expression) *"A regular expression, regex or regexp (sometimes called a rational expression) is, in theoretical computer science and formal language theory, a sequence of characters that define a search pattern."*

### How to combo Notepad++ and Regular expression
[With Notepad++ you can use regexp](http://docs.notepad-plus-plus.org/index.php/Regular_Expressions) e.g. in search patterns. So just open **Search -> Find...** and change **Search Mode** to **Regular expression**. Then input your pattern to **Find what :** field. 
![Notepadplusplus Find]({{ site.url }}/images/notepadplusplus_regexp_find.png)

#### Sample patterns
```
([0-9]+)
``` 
Find any number (e.g. 1023 or 7)
___
```
9([0-5])9
```
Find any of following: 909, 919, 929, 939, 949 or 959
___
```
([a-z]){5}
```
Find all words that only contain lowercase letters between a-z and have at least 5 chars 
___
```
\b([a-z]){5}\b
```
Find all words that only contain lowercase letters between a-z and have exactly 5 chars

#### Bonus
Find also has nice **Count** button that you can use to count matches. 
![Notepadplusplus Count]({{ site.url }}/images/notepadplusplus_regexp_count.png)