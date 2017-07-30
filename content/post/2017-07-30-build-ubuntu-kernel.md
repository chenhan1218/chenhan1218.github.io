+++
css = []
date = "2017-07-30T11:13:57+08:00"
description = ""
draft = false
highlight = true
scripts = []
title = "Build Ubuntu kernel"

+++

## Build Ubuntu 16.04 (Xenial) kernel on launchpad
```
git clone git://kernel.ubuntu.com/ubuntu/ubuntu-xenial.git
cd ubuntu-xenial
fakeroot debian/rules clean
debuild -S

# upload source package to launchpad
dput <Your ppa> ../linux_4.4.0-87.110_source.changes
```

## Build Ubuntu 16.04 (Xenial) HWE kernel on launchpad
```
git clone git://kernel.ubuntu.com/ubuntu/ubuntu-xenial.git
cd ubuntu-xenial
git checkout origin/hwe -b hwe
fakeroot debian/rules clean
debuild -S

# upload source package to launchpad
dput <Your ppa> ../linux-hwe_4.10.0-29.33~16.04.1_source.changes
```

## Build Ubuntu unstable kernel on launchpad
```
git clone git://kernel.ubuntu.com/ubuntu/unstable.git
cd unstable
fakeroot debian/rules clean
debuild -S

# upload source package to launchpad
dput <Your ppa> ../linux_4.13.0-2.3_source.changes
```
