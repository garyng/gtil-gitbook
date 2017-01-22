---
layout: post
title: 'Cake - Remove Solution Folder From .Projects Property'
tags: ['C#', 'Cake', '.NET']
categories: ['C#']
date: '2017-01-21 12:14'
author: 'GaryNg'
---

# Problem
`Cake`'s built-in .Projects properties will return solution folder.

# Solution
## Cake.Incubator
GitHub: https://github.com/cake-contrib/cake.incubator

GitBook: https://www.gitbook.com/book/wwwlicious/cake-incubator/details

```cs
// test.sln with 3 projects, proj1.csproj, solFldr, solFldr/proj2.csproj
var solution = ParseSolution(new FilePath("test.sln"));

// returns proj1.csproj, proj2.csproj
solution.GetProjects();

// returns proj1.csproj, solFldr, solFldr/proj2.csproj
solution.Projects;
```
from https://wwwlicious.gitbooks.io/cake-incubator/content/solution_extensions.html
