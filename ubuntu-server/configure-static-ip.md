---
title: Configuring a Static IP for Ubuntu Server
description: 
published: 1
date: 2022-07-03T03:48:33.535Z
tags: how-to, ip-address, networking, static-ip, netplan
editor: markdown
dateCreated: 2022-07-03T03:48:33.535Z
---

# 00-installer-config.yaml

````bash
network:
  version: 2
  renderer: networkd
  ethernets:
    ens3:
      dhcp4: no
      addresses:
        - 192.168.121.221/24
      gateway4: 192.168.121.1
      nameservers:
          addresses: [8.8.8.8, 1.1.1.1]
````