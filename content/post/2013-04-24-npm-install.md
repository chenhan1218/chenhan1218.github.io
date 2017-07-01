---
title: 'npm install'
date: "2013-04-24 16:00:00"
comments: true
categories: 
---


NPM (Node Packaged Modules) 是 Node.js 裡很好用的模組安裝工具。從 npm 1.0 開始，有兩個方式來安裝模組。

1. 全域安裝，通常會把模組安裝在 /usr/local/lib/node_modules 的位置。
``` bash
$ npm install -g express
``` 

2. 專案資料夾內的安裝，
``` bash
$ npm install express
``` 

如何決定要用什麼方式來安裝呢。Node.js 提供了以下的原則：

1. 如果你要安裝的模組是用在專案中，以 require('whatever') 的方式來引用。那麼就在專案的資料夾安裝
2. 如果你安裝的模組是要在 shell 裡使用的，那麼就用全域安裝。

不過，有些模組你既需要在專案中 require 它，也需要在 shell 中執行它所附加的小工具。像是常用的[Coffee-script](http://coffeescript.org/)、[Express](http://expressjs.com/)。
那該怎麼做比較好呢。我建議你在全域還有專案資料夾內各安裝一份，這樣子很簡單也容易維護。

P.S. 你可以用 npm -v 來確定自己的 npm 是否為1.0 以上的版本。

Ref:
[npm 1.0: Global vs Local installation](http://blog.nodejs.org/2011/03/23/npm-1-0-global-vs-local-installation/)