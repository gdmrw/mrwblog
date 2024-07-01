---
title: Hugo Warning [found no layout file for ..]
date: 2024-07-01
showToc: true
UseHugoToc: false
tags: 
- hugo
- git
---

### Warning message:
```
WARN  found no layout file for "html" for kind "home": You should create a template file which matches Hugo Layouts Lookup Rules for this combination.
WARN  found no layout file for "html" for kind "taxonomy": You should create a template file which matches Hugo Layouts Lookup Rules for this combination.
WARN  found no layout file for "html" for kind "section": You should create a template file which matches Hugo Layouts Lookup Rules for this combination.
WARN  found no layout file for "html" for kind "page": You should create a template file which matches Hugo Layouts Lookup Rules for this combination.
WARN  found no layout file for "html" for layout "archives" for kind "page": You should create a template file which matches Hugo Layouts Lookup Rules for this combination.
WARN  found no layout file for "html" for layout "search" for kind "page": You should create a template file which matches Hugo Layouts Lookup Rules for this combination.
WARN  found no layout file for "html" for kind "term": You should create a template file which matches Hugo Layouts Lookup Rules for this combination.
WARN  found no layout file for "json" for kind "home": You should create a template file which matches Hugo Layouts Lookup Rules for this combination.
```

This will happen when you reclone repo with git submodule from remote branch and the `submodule` not get downloaded as well. In other words, Submodules may not get cloned automatically. 

### Solution:

```
git submodule init
git submodule update
```

[Source](https://stackoverflow.com/questions/60269683/how-to-fix-the-error-found-no-layout-file-for-html-for-page-in-hugo-cms)
