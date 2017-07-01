---
title: 'git subtree merge strategy'
date: "2013-05-01 16:00:00"
comments: true
categories: 
---

最近工作上遇到一個問題，我們希望在自己的專案中保有專案所依賴的函式庫，而不隨著函式庫的版本更新而變動。例如我們也許想使用
[boost 1.5.3](http://www.boost.org/users/history/version_1_53_0.html) 做為我們的依賴函式庫，未來等 [boost](http://www.boost.org/) 改版到 1.6 以後，也許先不急著更換，等到時機恰當再做更換。

在專案中保有的函式庫，檔案結構如：
```
project
├── lib
│   └── boost
└── src
    └── test.cpp
```

對於這樣的開發需求，我們可以採用 git 裡的 subtree 來幫助我們做到這件事。

** A. 將 lib 併入專案 **
``` 
$ git remote add -f boost /path/to/boost
$ git merge -s ours --no-commit boost/master
$ git read-tree --prefix=lib/boost/ -u boost/master
$ git commit -m "Merge boost as our subdirectory"
```

** B. 導入 lib 更新 **
```
$ rm -rf lib/project1
$ git add -u
$ git merge -s ours --no-commit boost/master
$ git read-tree --prefix=lib/boost/ -u boost/master
$ git commit -m "Merge boost as our subdirectory"
```

之所以採用 git subtree，而不採用 git submodule。是因為 git submodule 的更新原則基本上是會更新到最新的版本，以我們的開發需求並不適用。

Ref: 

1. [How to use the subtree merge strategy](https://www.kernel.org/pub/software/scm/git/docs/howto/using-merge-subtree.html)
2. [Working with subtree merge](https://help.github.com/articles/working-with-subtree-merge)
