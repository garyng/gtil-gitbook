---
layout: post
title: 'Testing npm package locally'
tags: ['']
categories: ['']
date: '2017-01-25 00:36'
author: 'GaryNg'
---

# Solution
In project folder (eg: `test-package`):
```bash
npm link
```

In project using the `test-package`:
```
npm link test-package
```

# To `unlink`
In `test-package`
```bash
npm unlink
```

# Reference
[Using npm link to use node modules that are "in progress"](https://egghead.io/lessons/node-js-using-npm-link-to-use-node-modules-that-are-in-progress)

[Simple Way to Manage Local Node Modules Using NPM Link](https://60devs.com/simple-way-to-manage-local-node-module-using-npm-link.html)
