---
title: '利用 RTL-SDB 接收 ads-b 訊號'
date: "2017-07-01 05:21:00"
comments: true
categories: 
---
Automatic dependent surveillance – broadcast (ADS–B) 是
廣播式自動回報監視（ADS-B）

周末跟同事借了 RTL-SDB 來玩。

無論使用哪種方式啟動，都要先確定一些 driver 不會被自動載入。設定 driver blacklist 後，重開機讓設定生效。
```
$ cat << EOF > /tmp/blacklist-rtl-sdr.conf
blacklist dvb_usb_rtl28xxu
blacklist e4000
blacklist rtl2832
EOF
$ sudo mv /tmp/blacklist-rtl-sdr.conf /etc/modprobe.d
$ sudo reboot
```

接下來可以選擇使用 docker 或 snap 來啟動 dump1090
## Docker
我的測試環境是 Debian 9.0 Stretch AMD64

使用 docker 來執行 docker hub 上己經包好的 dump1090
```
docker run --rm --it -p 8080:8080 --device=/dev/bus/usb inodes/docker-x86-rtlsdr-dump1090 --net
```
連接到 http://localhost:8080 就可以看到接收到的飛機訊號

## Snap
我的測試環境是 Ubuntu 16.04 Xenial AMD64

安裝 adsb-box 並連接 snap interface。最後重新啟動服務
```
sudo snap install --beta adsb-box

sudo snap connect adsb-box:raw-usb
sudo snap connect adsb-box:process-control
sudo snap connect adsb-box:system-observe
sudo snap connect adsb-box:network-observe
sudo systemctl restart snap.adsb-box.dump1090.service
sudo systemctl restart snap.adsb-box.piaware.service
```
連接到 http://localhost:8080 就可以看到接收到的飛機訊號

[1] [飛航服務總臺 > 設施介紹 > 監視裝備](http://www.anws.gov.tw/cht/index.php?code=list&ids=25)
[2]