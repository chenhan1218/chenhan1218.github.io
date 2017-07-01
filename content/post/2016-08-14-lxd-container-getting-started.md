---
title: 'LXD container Getting Started'
date: "2016-08-14 04:04:00"
comments: true
categories: 
---
Below I give some simple command to run a ubuntu:16.04 lxd container. LXD container is fast, very efficient, very low-footprint virtual machine. I recommend people who didn't need low-level system control (such as disk, loopback device) give it a try. I think this kind of lightweight virtual machine would benefit people who study machine learning or similar scientific computing.

```
# check current status of lxd. If you install lxd the first time, it should containing no virtual machines.
lxc list

# if my-ubuntu virtual machine not exist yet.
lxc launch ubuntu:16.04 my-ubuntu
# if my-ubuntu virtual machine already exist.
lxc start my-ubuntu

# check status of my-ubuntu virtual machine
lxc list

# login to root account
lxc exec first -- /bin/bash
# or login to ubuntu account
lxc exec first -- /bin/su - ubuntu

# stop the virtual machine
lxc stop my-ubuntu

# you can even copy virtual machine
lxc copy my-ubuntu my-ubuntu2
# or rename it
lxc mv my-ubuntu stanley-ubuntu
lxc mv stanley-ubuntu my-ubuntu

# delete my-ubuntu virtual machine
lxc delete my-ubuntu

# check my-ubuntu is deleted
lxc list
```

Varies images is provided by Canonical in http://images.linuxcontainers.org/

Note that lxd has some limitaions. Such as you can't
- setup loopback device
- mount fuse file system
- have bridged network.
- load/remove kernel module
...
(But if you choose to run a priviledged lxd virtual machine, some limitations might not exist anymore. But I haven't dig into it currently.)