---
layout: post
title: 'Backus-Naur Form'
tags: ['BNF', 'Computer Science', 'CS']
category: 'computer science'
date: '2017-03-26 20:58'
author: 'GaryNg'
---

# Backus-Naur Form
Came across BNF while I was browsing [ZenSharp](https://github.com/ulex/ZenSharp) repo on GitHub.

BNF is used by `ZenSharp` for defining its live template language: [Templates.ltg](https://github.com/ulex/ZenSharp/blob/master/ZenSharp.Integration/Templates.ltg)

## BNF
BNF is a metalanguage (language that used to talk about a language) used to describe the grammar of a programming language.

## Symbols
`<>`: angle brackets indicate a _nonterminal_ that needs to be further expanded

`::=`: _is defined as_

`|`: _or_

## Reference

[The language of languages](http://matt.might.net/articles/grammars-bnf-ebnf/)

[https://www.cis.upenn.edu/~matuszek/cit594-2014/Lectures/16-bnf.ppt](https://www.cis.upenn.edu/~matuszek/cit594-2014/Lectures/16-bnf.ppt)

[What is BNF notation?](http://cuiwww.unige.ch/db-research/Enseignement/analyseinfo/AboutBNF.html)

[Backus-Naur Form (BNF)](http://www.ee.usyd.edu.au/tutorials/adatute/bnf.html)

## See Also
[ZenSharp](https://github.com/ulex/ZenSharp): ZenSharp for ReSharper is mnemonics on steroids!


## Others
Syntax support in Atom: [language-bnf](https://atom.io/packages/language-bnf)
