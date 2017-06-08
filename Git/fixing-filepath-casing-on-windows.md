---
layout: post
title: 'Fixing Filepath Casing on Windows'
tags: ['Git']
category: 'git'
date: '2017-03-04 23:42'
author: 'GaryNg'
---

# Fixing Filepath Casing on Windows
## Problem
Just found this weird problem on my GitBook (Built by Travis):  
![](../images/posts/fixing-filepath-casing-on-windows/2017-03-04_235518.png)  

Turn out that on GitHub, there are two folders: `Others` and `others` (different casing)  
![Folder of same name with different casing](../images/posts/fixing-filepath-casing-on-windows/2017-03-04_234410.png)

But it shows as one folder on my Windows machine:
![Shows as one folder only on Windows](../images/posts/fixing-filepath-casing-on-windows/2017-03-04_234716.png)

## Solution
Some Googling brought me to this post [Git Unite – Fix Case Sensitive File Paths on Windows](http://www.woodcp.com/2013/01/git-unite-fix-case-sensitive-file-paths-on-windows/)
> Since Windows is **not case sensitive**, the git index case sensitivity issue does not manifest itself until browsing the code repository on GitHub or cloning the repository to a case sensitive file system on Linux.

Using the tool [Git.Unite](https://github.com/tawman/git-unite) solved the problem:  
![Screenshot of running Git.Unite ](../images/posts/fixing-filepath-casing-on-windows/2017-03-04_235250.png)

# Reference
[Git Unite – Fix Case Sensitive File Paths on Windows](http://www.woodcp.com/2013/01/git-unite-fix-case-sensitive-file-paths-on-windows/)  
[Git.Unite on GitHub](https://github.com/tawman/git-unite)
