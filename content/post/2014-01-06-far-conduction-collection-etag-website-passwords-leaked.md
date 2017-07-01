---
title: '遠傳電收 eTag 網站密碼外洩'
date: "2014-01-06 16:00:00"
comments: true
categories: 
---
遠傳電收 eTag 網站出包，仔細看了一下，發現遠傳電收在資訊安全上犯了很基本的錯。提供服務的伺服器通常只允許客戶端存取特定資料夾以內的檔案。如果沒有過濾好，密碼等等重要檔案很容易就外洩。這種 Directory traversal 的防範通常在資安書籍的頭幾章就可以讀到了。

[遠通eTag網站被「真駭客」破解！伺服器密碼全部看光光](http://www.setnews.net/News.aspx?PageGroupID=4&NewsID=9661)