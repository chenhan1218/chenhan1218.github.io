---
title: 'git submodule'
date: "2013-05-05 16:00:00"
comments: true
categories: 
---


我們可以透過 git submodule 來組合眾多小專案、函式庫，形成一個大專案。這樣的流程特別常見於應用程式依賴於底層的Library時。
(例如Web App 可能會想要引用 [facebook-ios-sdk](http://github.com/facebook/facebook-ios-sdk))

使用 git submodule 要先掌握2件事

1. git 使用 .gitmodules 來對應小專案、函式庫於大專案中的資料夾位置。
2. 每個開發者可以自行管理要不要取出各個小專案，每個小專案的設定將被註冊在 .git/config

##Add submodule
```
git submodule add /path/to/library library/position/in/my_project
```

##Check-out submodule

其它協同開發者在大專案中準備取出小專案前，需要先 init, 把小專案的路徑依 .gitmodule 的內容，註冊到自己的 .git/config (如此，git 才知道怎麼去取出、更新小專案)
```
git submodule init
```
之後就可以開始更新小專案了。
```
git submodule update
```
或是加入 --recursive 參數，把小專案中的小專案也一併取出來
```
git submodule update --recursive
```

##Remove submodule
移除 submodule 時，修改 .gitmodules 的內容，將欲刪除的 submodule 設定刪掉，並將大專案中的小專案資料夾刪去。再 commit 即可。
```
# use vim to edit .gitmodules
vim .gitmodules
# remove 
rm -rf library/position/in/my_project
```

.git/config 內已註冊的小專案路徑，也可將它刪掉(非必要，但建議)。
```
# use vim to edit .git/config
vim .git/config
```

Ref:

1. [Git Submodules: Adding, Using, Removing, Updating](http://chrisjean.com/2009/04/20/git-submodules-adding-using-removing-and-updating/)
2. [Git Submodule 的認識與正確使用！](http://josephjiang.com/entry.php?id=342)