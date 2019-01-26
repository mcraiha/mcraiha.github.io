---
layout: post
title:  "Slash vs. Backslash in Azure DevOps scripting"
date:   2019-01-26 16:20:00 +0200
categories: slash backslash Azure DevOps
---
When one of your foot is in Windows land, it is easy to make mistakes when trying to do cross platform scripting. Cross platform in this case means **Azure DevOps** [Builds pipeline](https://azure.microsoft.com/en-us/services/devops/pipelines/).

When you do pipelines in Azure DevOps, you can select the operating system where you want the process to run. Since Linux instances are usually faster to complete operations where files are processed, I usually choose that.

Under Windows, one can easily create nice echo script, that writes current time to file.

```terminal
echo %date% %time% > output/buildinfo.txt
```
or
```terminal
echo %date% %time% > output\buildinfo.txt
```
and both of these will work fine under Windows. But first one will just output *%date% %time%* to right place when run in Ubuntu host. And second one will write same to wrong file since in most Unix filesystems \ aka backslash is a [valid character](https://en.wikipedia.org/wiki/Ext3) for filename and not a path separator. 

And when you create a task in Azure DevOps, it doesn't even give you a warning about this. And it doesn't give you a warning when you run it.
