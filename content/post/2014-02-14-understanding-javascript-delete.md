---
title: 'Understanding Javascript Delete'
date: "2014-02-14 01:58:00"
comments: true
categories: 
---
[Understanding delete](http://perfectionkills.com/understanding-delete/)
這篇文章討論 Javascript 的 delete 行為，並且釐清一些常見的誤解。全文很長，最後總結是精華，我把它整理翻譯後分享出來如下。

* 變數跟函式宣告都是屬性。他們會是Activation Object(啟動物件)的屬性。或是Global Object(全域物件)的屬性。
* 屬性具有 attributes (像是 ReadOnly, DontEnum, DontDelete and Internal，可視為一種旗標)。其中 DontDelete 是負責表示這項屬性可否被刪除的 attribute
* 不管在全域或是函式作用域中，變數與函式宣告總是具有 DontDelete
* 函式參數是 Activation Object 的屬性，具有 DontDelete
* Eval code 裡的變數、函式宣告不具有 DontDelete
* 由配值(assignment)產出的屬性一定沒有任何 attributes ，也就不會有 DontDelete
* host 物件對 delete 的反應是無法預料的，他們想回應 true 或 false 都行

如果想更進一步了解，可以查閱 [ECMA-262 3rd edition specification](http://www.ecma-international.org/publications/files/ECMA-ST/Ecma-262.pdf).

其它相關Reference Link:
[stackoverflow - How to unset a Javascript variable?](http://stackoverflow.com/questions/1596782/how-to-unset-a-javascript-variable)