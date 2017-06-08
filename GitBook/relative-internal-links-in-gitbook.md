---
layout: post
title: 'Relative Internal Links in GitBook'
tags: ['links', 'GitBook']
category: 'gitbook'
date: '2017-06-08 18:04'
author: 'GaryNg'
---

# Relative Internal Links in GitBook
## Solution
```
[Link Text](../<folder>/<page>.md#<header>)
```

GitBook cli will convert `.md` link to `.html`

> Tip: Just copy from SUMMARY.md and add `../` infront of the link

## Example
[Git and Git Flow](../Git/git-and-git-flow.md)

## Note
This will not works with links that have spaces in them. For example:

```
[Backus-Naur Form](../Computer Science/backus-naur-form.md)
```
[Backus-Naur Form](../Computer Science/backus-naur-form.md)

The link will remain as `.md` link.

See issue [#1070 .md links are not converted when they have a space](https://github.com/GitbookIO/gitbook/issues/1070) on GitHub.

## Reference
[Learn GitBook - Internal Links](https://seadude.gitbooks.io/learn-gitbook/content/chapter1/internal.html)
