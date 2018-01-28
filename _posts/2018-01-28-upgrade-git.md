---
layout: post
title: Upgrade git
tags: mac homebrew terminal
date: 2018-01-28 16:02:00 -0400
comments: true
---

Prerequisites: [git](https://git-scm.com/) and [Homebrew](https://brew.sh/) installed on Mac OS X

1. Find version
```
$ git --version
```
2. Update Homebrew
```
$ brew update && brew upgrade
```
3. Install git, and brew will decide which stable version to use
```
$ brew install git
```
4. Force the link and overwrite all conflicting files
```
$ brew link --overwrite git
```
5. Check version and you will see the installed latest version
```
git version 2.16.1
```


