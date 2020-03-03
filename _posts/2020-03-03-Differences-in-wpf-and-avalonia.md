---
layout: post
title:  "Differences in WPF and Avalonia"
date:   2020-03-03 20:55:00 +0200
categories: XAML WPF Avalonia
---
# Differences in WPF and Avalonia

If you want create desktop application for Windows platform there are multiple UI frameworks you can use.

I have written some [WPF](https://en.wikipedia.org/wiki/Windows_Presentation_Foundation) code during my years, and this year I wanted to port my password manager to [Avalonia](https://avaloniaui.net/). Since both can now be done via .NET Core, I could just forget possible language differences between frameworks by using almost same base code for both frameworks and just focus my effort to UI parts.

Below are some things that are different in WPF and Avalonia

## Visibility vs. IsVisible

In WPF one can use `Visibility` in XAML to hide and collapse visual elements. But in Avalonia you have to use `IsVisible` and it is boolean (`true` means **visible** and `false` means **collapsed**).

```xml
<Grid Visibility="{Binding WizardVisibility}>
```
and
```csharp
public Visibility WizardVisibility
{ 
    get
    {
        return this.csc == null ? Visibility.Visible : Visibility.Collapsed;
    } 
    set
    {

    }
}
```

**vs.**

```xml
<Grid IsVisible="{Binding WizardVisibility}">
```
and
```csharp
public bool WizardVisibility
{ 
    get
    {
        return this.csc == null;
    } 
    set
    {

    }
}
```