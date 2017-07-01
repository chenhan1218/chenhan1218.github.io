---
title: '每個C語言開發者都要了解的 Undefined Behavior'
date: "2014-01-21 00:54:00"
comments: true
categories: 
---
在閱讀LLVM 部落格中的 [What Every C Programmer Should Know About Undefined Behavior #1/3](http://blog.llvm.org/2011/05/what-every-c-programmer-should-know.html) 後，決定簡短的記錄這系列文章的重點並且在seminar上分享出來。我認為這篇文章是C語言開發者在開發一段時間後必讀的文章。文章中提到許多的 undefined behavior 是很容易犯的錯。這之中牽涉到 compiler 進行的最佳化，使得撰寫C語言時必須注意一些細節，才能避免在最佳化的過程中，產生與預期不相同的執行結果。

<iframe src="//www.slideshare.net/slideshow/embed_code/36318298" width="427" height="356" frameborder="0" marginwidth="0" marginheight="0" scrolling="no" style="border:1px solid #CCC; border-width:1px 1px 0; margin-bottom:5px; max-width: 100%;" allowfullscreen> </iframe> <div style="margin-bottom:5px"> <strong> <a href="https://www.slideshare.net/ssusercd43c4/2014-0626-a-guide-to-undefined-behavior-in-c-and-c-stanley" title="2014-06-26 - A guide to undefined behavior in c and c++" target="_blank">2014-06-26 - A guide to undefined behavior in c and c++</a> </strong> from <strong><a href="http://www.slideshare.net/ssusercd43c4" target="_blank">辰翰 蕭</a></strong> </div>

如果需要中文翻譯的讀者，已有中國網友翻譯，可參考以下文章
1. [未定义行为：What Every C Programmer Should Know #1/3](http://sohulinux.blog.sohu.com/176185110.html)
2. [未定义行为：What Every C Programmer Should Know #2/3](http://sohulinux.blog.sohu.com/176211282.html)
3. [未定义行为：What Every C Programmer Should Know #3/3](http://sohulinux.blog.sohu.com/176282266.html)
4. [About Undefined Behavior[译文]](http://www.cnblogs.com/foohack/p/3582239.html)