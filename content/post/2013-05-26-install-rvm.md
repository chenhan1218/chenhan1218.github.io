---
title: 'Install RVM, Ruby and Gems without sudo permission'
date: "2013-05-26 16:00:00"
comments: true
categories: 
---

最近接觸 Ruby on Rails，把一些使用心得補上。

正如同很多進化中的語言，Ruby on Rails 經常會遇到函式庫版本、執行環境的管理問題。我們可以使用[Ruby Version Manager (RVM)](https://rvm.io/)來解決這個問題。
事實上我建議新手在第一次安裝 Ruby 前，就先安裝 RVM 來避免未來可能的問題。

這邊我示範如何在沒有 sudo 的權限下，安裝 RVM, Ruby, Rails Gem在自己的家目錄下。每位使用者獨力安裝自己的 Ruby Environment 有個好處，就是不會相互干擾，容易除錯。
我的環境是 Ubuntu 12.04，以下流程在 MAC OS 上也是可以運作的。(事實上這也是[Ruby Version Manager (RVM)](https://rvm.io/)所提供的預設安裝方法，這裡只是提供我的經驗給大家參考)

## 安裝 RVM, Ruby, Rails Gem 於 ~/.rvm

1- 安裝 RVM
```
# install rvm via internet.
curl -L https://get.rvm.io | bash -s stable
```

2- 用 RVM 來安裝 Ruby
```
# install ruby 1.9.3 with rvm
rvm install 1.9.3
```

3- 用 Ruby 所附加的 gem 工具來安裝 Rails
```
# install gem
gem install rails
```

## Ruby相依函式庫

但是要特別注意的是，在安裝 Ruby 的時候，因為 Ruby 依賴 OpenSSL, YAML 等等的函式庫，
如果你的電腦沒有這些函式庫，安裝 Ruby 時會遇到問題。有兩個方法來解決這個問題

#### 請系統管理員手動安裝相依函式庫
以 Ubuntu12.04 為例，需要安裝 libreadline6-dev, libyaml-dev, sqlite3, libxslt1-dev, libgdbm-dev, libffi-dev
然後依照上述步驟2，開始安裝 Ruby

#### 設定 RVM autolibs 為 enable
設定 autolibs 為 enable
```
rvm autolibs enable
```
然後依照上述步驟2，開始安裝 Ruby，此時，RVM會向你要求 sudo 權限，並安裝需要的函式庫。

Ref:

1. [How to install RVM debian requirements without giving sudo for rvm user. Answered by Chen-Han Hsiao](http://stackoverflow.com/questions/16563115/how-to-install-rvm-debian-requirements-without-giving-sudo-for-rvm-user/)
2. [RVM Autolibs](https://rvm.io/rvm/autolibs)
