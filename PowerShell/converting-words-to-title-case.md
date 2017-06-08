---
layout: post
title: 'Converting words to Title Case'
tags: ['PowerShell']
category: 'powershell'
date: '2017-02-02 19:56'
author: 'GaryNg'
---

# Converting words to Title Case
## Solution
```powershell
(Get-Culture).TextInfo.ToTitleCase("war and pEAce")
```

```
> War And Peace
```

### Note
Words entirely in **UPPER CASE** will not be converted  
Use `.ToLower()` first before converting
```powershell
(Get-Culture).TextInfo.ToTitleCase("WAR AND PEACE".ToLower())
```
```
> War And Peace
```

# Reference

\#PSTip How to convert words to Title Case: http://www.powershellmagazine.com/2013/07/24/pstip-how-to-convert-words-to-title-case/
