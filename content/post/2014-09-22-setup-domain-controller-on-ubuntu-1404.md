---
title: 'Setup Domain Controller on Ubuntu 14.04'
date: "2014-09-22 11:09:00"
comments: true
categories: 
---
在ubuntu 14.04 上架設 Samba Domain Controller 的步驟：
1. 安裝 samba libpam-smbpass
```
sudo apt-get install samba libpam-smbpass
```
samba 版本目前是4.1.6 (4.0以上的 Samba 才有提供 Domain Controller 的功能)
```
samba -V
Version 4.1.6-Ubuntu
```

2. 使用 samba-tool 一步一步設定，這裡我規劃 samba domain 的網域為 mysamba.test.io
```
samba-tool domain provision --use-rfc2307 --interactive
```

設定成功，過程的設定記錄如下：
```
vagrant@vagrant-ubuntu-trusty-64:~$ sudo samba-tool domain provision --use-rfc2307 --interactive                                                   
Realm: mysamba.test.io
 Domain [mysamba]: 
 Server Role (dc, member, standalone) [dc]: 
 DNS backend (SAMBA_INTERNAL, BIND9_FLATFILE, BIND9_DLZ, NONE) [SAMBA_INTERNAL]: 
 DNS forwarder IP address (write 'none' to disable forwarding) [192.168.1.253]: 192.168.1.253
Administrator password: 
Retype password: 
Looking up IPv4 addresses
More than one IPv4 address found. Using 192.168.1.2
Looking up IPv6 addresses
No IPv6 address will be assigned
Setting up secrets.ldb
Setting up the registry
Setting up the privileges database
Setting up idmap db
Setting up SAM db
Setting up sam.ldb partitions and settings
Setting up sam.ldb rootDSE
Pre-loading the Samba 4 and AD schema
Adding DomainDN: DC=mysamba,DC=test,DC=io
Adding configuration container
Setting up sam.ldb schema
Setting up sam.ldb configuration data
Setting up display specifiers
Modifying display specifiers
Adding users container
Modifying users container
Adding computers container
Modifying computers container
Setting up sam.ldb data
Setting up well known security principals
Setting up sam.ldb users and groups
Setting up self join
Adding DNS accounts
Creating CN=MicrosoftDNS,CN=System,DC=mysamba,DC=test,DC=io
Creating DomainDnsZones and ForestDnsZones partitions
Populating DomainDnsZones and ForestDnsZones partitions
Setting up sam.ldb rootDSE marking as synchronized
Fixing provision GUIDs
A Kerberos configuration suitable for Samba 4 has been generated at /var/lib/samba/private/krb5.conf
Setting up fake yp server settings
Once the above files are installed, your Samba4 server will be ready to use
Server Role:           active directory domain controller
Hostname:              vagrant-ubuntu-trusty-64
NetBIOS Domain:        MYSAMBA
DNS Domain:            mysamba.test.io
DOMAIN SID:            S-1-5-21-711469164-2329730621-2401598146
```

附註：在使用 samba-tool 的過程式如果有設定錯誤，想再進行一行 samba-tool 操作，會出現錯誤訊息，提示你必須把 /var/lib/samba/private/sam.ldb /etc/samba/smb.conf 刪除，讓 samba-tool 來重新建立
```
sudo rm /var/lib/samba/private/sam.ldb
sudo rm /etc/samba/smb.conf
```

Ref: [Samba AD DC HOWTO](https://wiki.samba.org/index.php/Samba_AD_DC_HOWTO)