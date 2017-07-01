---
title: '取得 Google API 金鑰'
date: "2014-08-01 05:27:00"
comments: true
categories: 
---
Google API 提供了很多好用的 API，可以用來存取Google 提供的資源(包含資料、運算資源等等)。之前貢獻了一個 patch 在 Hackfoldr 上，就是透過 YouTube Data API v3 去取得 Youtube 的影片相關資訊。要發佈使用Google API的專案時，就要記得先去取得一組 Google API 金鑰。步驟可參考Google的說明 (介面可能稍有不同，但差異應該不大)。

[取得 API 金鑰](https://developers.google.com/maps/documentation/javascript/tutorial?hl=zh-tw#api_key)  
如何建立 API 金鑰：

1. 請前往 API 控制台 (位於 https://code.google.com/apis/console)，並登入您的 Google 帳戶。
2. 按一下左選單中的 [Services] 連結。
3. 啟用 [Google Maps API v3] 服務。
4. 按一下左方選單中的 [API Access]。您可以從 [API Access] 頁面的 [Simple API Access] 區段取得 API 金鑰。Maps API 應用程式會使用 [Key for browser apps]。

根據預設，金鑰可用於任何網站。我們強烈建議您將金鑰限制於使用在自己管理的網域中，以免遭未經授權的網站使用。只要您按一下金鑰的 [Edit allowed referrers...] 連結，即可指定允許使用 API 金鑰的網域。

Referrers 就是允許向Google API發出請求的網域，如果你要發佈到 example.com，那麼就在這個欄位填寫 example.com/*。

再依照自己的需求，在[API 控制台](https://code.google.com/apis/console)打開相對應的API。以Hackfoldr來說，需要開啟 YouTube Data API v3 。

最後，把這組 API 金鑰配置到自已網站設定中。以Hackfoldr來說，就是填寫在 app/config.jsenv 中。這樣，網站應用程式就可以串接 Google API 來提供服務了。

註：Google API對每一個專案有流量上限。如果流量到達了就無法繼續使用，這時可以參考付費方案，來購買更多的使用量。