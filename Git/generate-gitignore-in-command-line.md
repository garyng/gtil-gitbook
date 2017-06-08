---
layout: post
title: 'Generate .gitignore in Command Line'
tags: ['Git','.gitignore']
category: 'git'
date: '2017-01-22 20:27'
author: 'GaryNg'
---

# Generate .gitignore in Command Line
## Installing
From [.gitignore.io](https://www.gitignore.io/docs)

```bash
git config --global alias.gi '!gi() { curl -L -s https://www.gitignore.io/api/$@ ;}; gi'
```

## Usage

```bash
git gi node > .gitignore
```
