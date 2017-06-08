---
layout: post
title: 'Disable StyleCop in Visual Studio'
tags: ['visual studio', 'stylecop']
category: 'visual studio'
date: '2017-06-08 13:20'
author: 'GaryNg'
---

# Visual Studio Disable StyleCop
## Solution

```xml
<StyleCopSettings Version="105">
  <GlobalSettings>
    <BooleanProperty Name="RulesEnabledByDefault">False</BooleanProperty>
  </GlobalSettings>
</StyleCopSettings>
```

Save as `Settings.stylecop` and place it in the folder next to the `.sln` file.
