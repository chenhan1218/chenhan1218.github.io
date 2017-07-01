---
title: 'backports driver'
date: "2015-09-17 03:12:00"
comments: true
categories: 
---
```
git clone git://git.kernel.org/pub/scm/linux/kernel/git/backports/backports.git
git clone git://git.kernel.org/pub/scm/linux/kernel/git/next/linux-next.git
cd backports/
./gentree.py --clean --git-revision next-20150525 ../linux-next/ release

cd release/
make menuconfig
make
```