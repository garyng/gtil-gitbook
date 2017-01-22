---
layout: post
title: 'Git and Git Flow'
tags: ['Git', 'Git Flow']
categories: ['Git']
date: '2017-01-20 23:46'
author: 'GaryNg'
---

Collections of `git` commands and workflow

# Git Commands

## Cleaning

### Dry run
```
git clean -n
```

### Interactive mode
```
git clean -i
```  
can be combined with other options

### Remove directories
```
git clean -d
```

### Remove ignored files
```
git clean -x -i
```

SO: [How to remove local (untracked) files from the current Git branch?](http://stackoverflow.com/a/64966/1023180)


## Branch

### Delete local branch
```
git -d <branch>
```

### Delete remote branch
**_Warning! Dangerous!_**
```
git push origin :<branch>
```

### Renaming a branch
SO: [How to rename a local Git branch?](http://stackoverflow.com/a/6591218/1023180)
```
git branch -m <old name> <new name>
```  

or to rename current branch:  
```
git branch -m <new name>
```  

### Cloning specific branch
SO: [How to clone a single branch in git?](http://stackoverflow.com/a/9920956/1023180)


# Git Workflow

WIP
