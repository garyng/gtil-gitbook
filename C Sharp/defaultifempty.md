---
layout: post
title: 'DefaultIfEmpty'
tags: ['C#']
category: 'C#'
date: '2017-02-12 23:35'
author: 'GaryNg'
---

# .DefaultIfEmpty()
Replace a collection with a default value
```cs
using System;
using System.Collections.Generic;
using System.Linq;

class Program
{
    static void Main()
    {
        // Empty list.
        List<int> list = new List<int>();
        var result = list.DefaultIfEmpty();

        // One element in collection with default(int) value.
        foreach (var value in result)
        {
            Console.WriteLine(value);
            // output: 0
        }

        result = list.DefaultIfEmpty(-1);

        // One element in collection with -1 value.
        foreach (var value in result)
        {
            Console.WriteLine(value);
            // output : -1
        }
    }
}

```


# Reference
[C# DefaultIfEmpty Method - Dot Net Perls](https://www.dotnetperls.com/defaultifempty)

SO: [Sequence contains no elements exception in linq without even using Single](http://stackoverflow.com/a/8867931/1023180)
