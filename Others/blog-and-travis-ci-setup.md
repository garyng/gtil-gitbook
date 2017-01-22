---
layout: post
title: 'Blog and Travis CI Setup'
tags: ['Others','Blog']
categories: ['Others']
date: '2017-01-20 22:52'
author: 'GaryNg'
---

# About this Blog
This blog (actually, the whole `gtil` repo) was inspired by [think()](https://github.com/zypeh/think) from [@zypeh](https://github.com/zypeh) and it is powered by ~~[vue-ghpages-blog](https://github.com/viko16/vue-ghpages-blog)~~ Gitbook.


# Deploy via Travis CI
## References
Mainly from [Auto-deploying built products to gh-pages with Travis](https://gist.github.com/domenic/ec8b0fc8ab45f39403dd)  
Unfortunately `travis encrypt-file` doesn't generate the correct key under Windows machine (see https://docs.travis-ci.com/user/encrypting-files/#Caveat ).   
GitHub API token can be used instead: [Automatically Update Github Pages with Travis](http://www.steveklabnik.com/automatically_update_github_pages_with_travis_example/)

```bash
travis encrypt GH_TOKEN=[the token you created before] --add
```

May also need: [Generating a new SSH key and adding it to the ssh-agent](https://help.github.com/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent/)


### Installing Travis
Using **[Chocolatey](https://chocolatey.org/install)** to install Ruby
```
iwr https://chocolatey.org/install.ps1 -UseBasicParsing | iex
```
Remember to run PowerShell as _**admin**_  
`Set-ExecutionPolicy RemoteSigned -Scope Process` if PowerShell refuse to install

```bash
choco install ruby
```

```bash
gem install travis
```  

sidenote: string with a colon followed by a space in .yml will fail the parser...
```
...
- git commit -m "chore(deploy): deploy from Tarvis CI"
...
```

### RubyGems SSL Certificate Updartes
Refer to http://guides.rubygems.org/ssl-certificate-update/  


# Editor
[Atom](https://atom.io/)  
Sublime Text 3? - Poor support for Chinese Language

## Plugins for editing Markdown files
- [markdown-writer](https://atom.io/packages/markdown-writer)
  - Able to customize config for each project (docs: https://github.com/zhuochun/md-writer/wiki/Settings-for-individual-projects)!
  - Ctrl + Shift + P > Markown Writer: Create Project Configs
- [tool-bar-markdown-writer](https://atom.io/packages/tool-bar-markdown-writer) which depends on [tool-bar](https://atom.io/packages/tool-bar)
- [markdown-preview](https://atom.io/packages/markdown-preview)

## Git Plugin
- [git-plus](https://atom.io/packages/git-plus)
