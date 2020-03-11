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

## Label vs. TextBlock

In WPF you can show text in window with `Label` control. Avalonia does not have that, so you have to use `TextBlock` instead. And `Content` becomes `Text`.

```xml
<Label Content="Length of generated password:" Margin="2,5,2,2" />
```
vs.
```xml
<TextBlock Text="Length of generated password:" Margin="2,5,2,2" />
```

## Clipboard vs. Application.Current.Clipboard

With WPF you can copy text to clipboard with `Clipboard.SetText` but with Avalonia you have to use `Application.Current.Clipboard.SetTextAsync` (and you should do `await` since it is an async method)

```csharp
Clipboard.SetText("A nice text");
```
vs.
```csharp
Application.Current.Clipboard.SetTextAsync("A nice text");
```

## ShowDialog needs owner

Going with WPF, one can show modal window with `ShowDialog`. Avalonia also has ShowDialog, but it needs to know owner when called. Luckily you can figure out the main window with some additional code. 

```csharp
CreatePasswordWindow passwordWindow = new CreatePasswordWindow(null);
passwordWindow.ShowDialog();
```
vs.
```csharp
CreatePasswordWindow passwordWindow = new CreatePasswordWindow();
if (Application.Current.ApplicationLifetime is IClassicDesktopStyleApplicationLifetime desktopLifetime)
{
    passwordWindow.ShowDialog(desktopLifetime.MainWindow);
}
```

## FindControl is needed for x:Name

In WPF universe using controls created in XAML via code is quite easy, if you just give those controls `x:Name`. But *"Unfortunately, Avalonia XAML rendering engine won't generate strongly typed x:Name references to controls"* so in Avalonia you have to use `FindControl` instead.

So if XAML part would be following
```xml
<TextBlock Text="Hello, world!" x:Name="MyTextBlock" />
```

then in WPF you would do
```csharp
MyTextBlock.Text = "New Text";
```

but in Avalonia it would be
```csharp
TextBlock textBlock = this..FindControl<TextBlock>("MyTextBlock");
textBlock.Text = "New Text";
```