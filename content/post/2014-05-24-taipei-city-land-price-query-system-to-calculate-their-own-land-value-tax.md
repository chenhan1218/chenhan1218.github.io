---
title: '利用台北市地價查詢系統 計算自用住宅土地地價稅'
date: "2014-05-24 15:33:00"
comments: true
categories: 
---
在 [中華民國內政部地政司全球資訊網-資訊與服務-地政相關系統查詢->公告土地現值](http://www.land.moi.gov.tw/chhtml/landvalue.asp?cid=100) 可以連結到各縣市的地政系統，查詢各地的公告土地現值、公告地價。

我們先來了解公告土地現值與公告地價的不同，根據[公告地價 - Wikipedia](http://zh.wikipedia.org/zh-tw/%E5%85%AC%E5%91%8A%E5%9C%B0%E5%83%B9)
* 公告土地現值作為土地移轉或設定典權時之參考；並作為主管機關審核土地移轉現值（例如官司糾紛時）及補償徵收土地地價之依據
* 公告地價作為土地所有權人申報地價之參考，政府依據土地所有權人所申報之地價課徵地價稅。

簡單的說在稅務上來說，公告土地現值是土地移轉時的土地價值依據，公告地價是課徵持有稅時的地價依據。[1]

其中以[臺北市地價查詢多功能服務系統](http://w2.land.taipei.gov.tw/query/prc/Input_p_addr.asp)為例，它同時提供了以地號查詢、以門牌查詢的功能。進入系統實際查詢，假設某地查詢結果為：
* 103年公告現值(元/平方公尺)：81,400
* 102年公告地價(元/平方公尺)：20,700

某屋主持有自用住宅土地 8坪，約為26.45平方公尺，根據目前地價稅自用稅率 0.12% 來計算：
```
公告地價*持分土地面積*稅率=地價稅
20700*26.45*0.0012=657
```
可知這位屋主一年需負擔的地價稅為 657元。[2]

事實上，永慶房屋也提供了[試算服務](http://www.yungching.com.tw/cb/CB040203.asp)，只要輸入每筆地號土地總面積、所有權人持分、當期申報地價，就可以試算出當年需繳交的地價稅。

[1] 對於公告地價、公告土地現值的定義是目前我的理解，如果有錯的地方歡迎大家糾正我。
[2] 透過這樣的公式，確實很容易就可以計算出需繳交的地價稅。不過還是要注意自己的持有土地是否申請為自用住宅用地，這方面就需要去請地政士或行政部門做更進一步的了解。如果土地用途不是申請為自用住宅，那麼一般稅率則是1%。