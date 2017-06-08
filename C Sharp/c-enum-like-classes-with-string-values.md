---
layout: post
title: 'C# enum-like Classes With String Values'
tags: ['C#']
category: 'C#'
date: '2017-03-22 23:02'
author: 'GaryNg'
---

# C# enum-like Classes With String Values

## Problem
This won't work for enum:

```csharp
enum GroupTypes
{
    TheGroup = "OEM",
    TheOtherGroup = "CMB"
}
```

## Solution
```csharp
public class LogCategory
{
 private LogCategory(string value) { Value = value; }

 public string Value { get; set; }

 public static LogCategory Trace { get { return new LogCategory("Trace"); } }
 public static LogCategory Debug { get { return new LogCategory("Debug"); } }
 public static LogCategory Info { get { return new LogCategory("Info"); } }
 public static LogCategory Warning { get { return new LogCategory("Warning"); } }
 public static LogCategory Error { get { return new LogCategory("Error"); } }
}
```

### Usage
```csharp
public static void Write(string message, LogCategory logCategory)
{
   var log = new LogEntry { Message = message };
   Logger.Write(log, logCategory.Value);
}
```

## Reference
SO: [Associating enums with strings in C#](http://stackoverflow.com/a/1343517/1023180)
