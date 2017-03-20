---
layout: post
title: 'Using Consolas Font in CMD'
tags: ['Windows', 'Others']
categories: ['Others']
date: '2017-03-21 00:35'
author: 'GaryNg'
---
# Using Consolas Font in CMD
> Using `Developer Command Prompt for VS2017` as an example  
> Remember to start it as **Administrator**

## Adding Consolas font to Regedit
Open `regedit`

Goto `HKLM\Software\Microsoft\Windows NT\CurrentVersion\Console\TrueTypeFont`

Add a `REG_SZ` entry with the following contents:  
Name = `00`  
Value = `Consolas`

![Adding Consolas font in regedit](../images/posts/using-consolas-font-in-cmd/2017-03-21_010655.png)

> NOTE: if there is already an entry for “00” you don’t need to change it. Simply  use “000” instead.

> Value has
to match the font name as seen at the following registry key:  
`HKLM\Software\Microsoft\Windows NT\CurrentVersion\Fonts`

[Optional] Log out and log in again / Restart

## Changing CMD's Fonts
Just go to Properties > Font and select `Consolas`

If `Consolas` is not found:   
![Consolas not found in the Font listbox](../images/posts/use-consolas-font-in-cmd/2017-03-21_005334.png)

Change code page to `850` or `65001`:
```bash
chcp 850
```
![Change code page to 850](../images/posts/use-consolas-font-in-cmd/2017-03-21_005458.png)

Try again

![Select Consolas in the Font listbox](../images/posts/using-consolas-font-in-cmd/2017-03-21_005657.png)

Change code page back to `936` (or whatever it is originally)
```bash
chcp 936
```
![](../images/posts/using-consolas-font-in-cmd/2017-03-21_010039.png)

## Error Updating Shortcut
![Error Updating Shortcut](../images/posts/using-consolas-font-in-cmd/2017-03-21_005808.png)

Solution: Restart command promt as **Administrator** and retry

# Reference
[Using Meslo LG with the Windows Console](https://github.com/andreberg/Meslo-Font/wiki/Using-Meslo-LG-with-the-Windows-Console)
