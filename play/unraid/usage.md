---
title: unraid 插件
categories: 
	- [play,unraid]
tags:
	- unriad
date: 2020/12/11 00:00:00
update: 2020/12/11 00:00:00
---

# 插件

```shell
$ vi /etc/hosts
199.232.68.133 raw.githubusercontent.com

# Plugin
https://github.com/dlandon/unassigned.devices/raw/master/unassigned.devices.plg
https://raw.githubusercontent.com/Squidly271/community.applications/master/plugins/community.applications.plg
```

# VFIO

```shell
vfio-pci.ids=054c:0899
```

# Problems

## Requested operation is not valid: cannot undefine domain with nvram

```shell
$ virsh undefine --nvram "Macinabox BigSur"
```

# 设置 DNS

```shell
$ vim /boot/config/go
echo "nameserver 8.8.8.8" >> /etc/resolv.conf
echo "nameserver 4.4.4.4" >> /etc/resolv.conf
```

