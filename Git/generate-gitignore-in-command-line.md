---
layout: post
title: 'Generate .gitignore in Command Line'
tags: ['Git','.gitignore']
categories: ['Git']
date: '2017-01-22 20:27'
author: 'GaryNg'
---

# Installing
From [.gitignore.io](https://www.gitignore.io/docs)

```bash
git config --global alias.gi '!gi() { curl -L -s https://www.gitignore.io/api/$@ ;}; gi'
```

# Usage

```bash
git gi node > .gitignore
```
