---
title: 'use snapper to Travel back in time and compare (The ultimate snapshot tool for Linux)'
date: "2016-08-16 04:13:00"
comments: true
categories: 
---
[Snapper](http://snapper.io/) is a great tool for making snapshot on linux. You can download it on ArchLinux/Debian/OpenSUSE/Ubuntu

Personally I use btrfs as  underlying file system. Here are some basic command to snapshot my data.

```
# install snapper
sudo apt install -y snapper

# Suppose /dev/sda3 is formatted as btrfs file system.
# mount the file system
sudo mount /dev/sda3 /mnt

# create a btrfs subvolme "data"
sudo btrfs subvolume create /mnt/data
# unmount /dev/sda3
sudo umount /mnt

# mount only the subvolume "data", instead of whole file system
sudo mount -o subvol=data /dev/sda3 /data

# create the snapper config for "/data" folder. The config name could be anything, here I choose "data"
sudo snapper -c data create-config /data

# By default, the snapper will make a snapshot per hour, just like Mac OS's Time machine.
# Check the snapshot list
# sudo snapper -c data list 
Type   | #    | Pre # | Date                            | User | Cleanup  | Description | Userdata
-------+------+-------+---------------------------------+------+----------+-------------+---------
single | 1 |       | Tue 16 Aug 2016 09:17:02 AM CST | root | timeline | timeline    |         
single | 2 |       | Tue 16 Aug 2016 10:17:02 AM CST | root | timeline | timeline    |         
single | 3 |       | Tue 16 Aug 2016 11:17:03 AM CST | root | timeline | timeline    |         
single | 4 |       | Tue 16 Aug 2016 12:17:03 PM CST | root | timeline | timeline    |      

# In fact, you can find the underlying snapshot in "data" subvolume
sudo mount /dev/sda3 /mnt
ls -al /mnt/data/.snapshots/
drwxr-x--- 1 root root 230 Aug 16 12:17 ./
drwxr-xr-x 1 root root 340 Aug 15 10:47 ../
drwxr-xr-x 1 root root  32 Aug 16 09:17 1/
drwxr-xr-x 1 root root  32 Aug 16 10:17 2/
drwxr-xr-x 1 root root  32 Aug 16 11:17 3/
drwxr-xr-x 1 root root  32 Aug 16 12:17 4/
```

If your root file system is also a btrfs subvolume. That would be even better. You can snapshot your whole system!
```
sudo snapper -c root create-config /
```