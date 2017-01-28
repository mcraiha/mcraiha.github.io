---
layout: post
title:  "Format your code when posting online"
date:   2017-01-28 16:30:00 +0200
categories: code formatting format gist github
---
# Format your code when you are posting it online
**Warning**, semirant incoming

There are multiple ways to post code online. And most of them should be banned!

Sample code shown in here is copied+pasted from **[Dot Net Perls](https://www.dotnetperls.com/fibonacci)**

&nbsp;

## The worst(tm) possible way to paste code
This award goes to anyone that takes a screenshot from badly formatted code and pastes that screenshot to forum/blog/IM.

![Worst code pasting]({{ site.url }}/images/worst_code_paste.png)

**Why this is bad:**

* It is hard to read the code (neither formatting nor folding)
* It is hard to copy+paste code
* It is hard to directly call that code

&nbsp;

## Bad way to paste code
This award goes to anyone that takes a screenshot from formatted code and pastes that screenshot to forum/blog/IM.

![Bad code pasting]({{ site.url }}/images/bad_code_paste.png)

**Why this is bad:**

* It is hard to copy+paste code
* It is hard to directly call that code

&nbsp;

## Horrible way to paste code
This award goes to anyone that just dumps code to plain textinput. Output is then assumed to be regular text.

using System;

class Program
{
public static int Fibonacci(int n)
{
int a = 0;
int b = 1;
// In N steps compute Fibonacci sequence iteratively.
for (int i = 0; i < n; i++)
{
int temp = a;
a = b;
b = temp + b;
}
return a;
}

static void Main()
{
for (int i = 0; i < 15; i++)
{
Console.WriteLine(Fibonacci(i));
}
}
}

**Why this is bad:**

* It is hard to read the code (neither formatting nor folding)
* It is hard to directly call that code

&nbsp;

## Mediocre way to paste code
This award goes to anyone that pastes code with folding but does NOT use color coding.

```
using System;

class Program
{
    public static int Fibonacci(int n)
    {
        int a = 0;
        int b = 1;
        // In N steps compute Fibonacci sequence iteratively.
        for (int i = 0; i < n; i++)
        {
            int temp = a;
            a = b;
            b = temp + b;
        }
        return a;
    }

    static void Main()
    {
        for (int i = 0; i < 15; i++)
        {
            Console.WriteLine(Fibonacci(i));
        }
    }
}
```

**Why this is bad:**

* It is not easy to read the code
* It is hard to directly call that code

&nbsp;

## Good way to paste code online
This award goes to anyone that pastes code with proper formatting and folding to forum/blog/IM.

```csharp
using System;

class Program
{
    public static int Fibonacci(int n)
    {
        int a = 0;
        int b = 1;
        // In N steps compute Fibonacci sequence iteratively.
        for (int i = 0; i < n; i++)
        {
            int temp = a;
            a = b;
            b = temp + b;
        }
        return a;
    }

    static void Main()
    {
        for (int i = 0; i < 15; i++)
        {
            Console.WriteLine(Fibonacci(i));
        }
    }
}
```

**Why this is bad:**

* It is hard to directly call that code

&nbsp;

## Better way to paste code online
This award goes to anyone that pastes code to gist (or similar service) and links that to the post.
<script src="https://gist.github.com/mcraiha/855bf8e36754a9af1ac8926660f258a1.js"></script>

&nbsp;

## Why I am complaining about this

It is sad to see so many blogs, forum posts etc. where the original poster has NOT used extra 30 seconds to make his/her code more readable and/or useable. 

Fortunately there are some services that have taken many extra steps to make sure that everything is super smooth. Like **[Rust Playground](http://play.integer32.com/)** which has folding, formatting and gist all build-in. Amazing job!  