---
title: Securing the Open SSH Server
description: Tips on how to better secure your SSH server from unauthorized access
published: 1
date: 2022-07-02T05:53:44.139Z
tags: how-to, openssh, openssh-server, security, ssh, ubuntu-server
editor: markdown
dateCreated: 2022-07-01T00:04:26.056Z
---

## Create a Backup of the Original File

<br>

````bash
sudo cp /etc/ssh/sshd_config /etc/ssh/sshd_config.original
````

<br>

## X11 Forwarding

<br>

**Turn off X11 forwarding if not needed**
````bash
X11Forwarding no
````

<br>

## Disable rhosts

<br>

**Rhosts was a weak method to authenticate systems. It defines a way to trust another system simply by the IP address.**
````bash
IgnoreRhosts yes
````

<br>

## DNS Hostname Checking

<br>

**By default, the SSH server can check if the client connecting maps back to the same combination of hostname and IP address.**
````bash
UseDNS yes
````

<br>

## Disable Empty Passwords
````bash
PermitEmptyPasswords no
````

<br>

## Max authentication attempts

<br>

**This option helps better defend against brute-force password attacks**
````bash
MaxAuthTries 3
````

## Public key authentication

<br>

**The best way to protect your ssh-server is to authenticate using keys.**
````bash
PubkeyAuthentication yes
PasswordAuthentication no
````

<br>

## Disable root login
````bash
PermitRootLogin no
````

<br>

## Set ssh protocol

<br>

**Put at the very end of the file**
````bash
Protocol 2
````

<br>


## Limit Who can login and what groups

<br>

**Create a special group with only the users you want to have access to logging in via ssh to your server.**
````bash
AllowGroups ssh-allow
AllowUsers ryan bob bill
````

<br>

## Use HashKnownHosts

<br>

**Previously it was common to store the hostname related to the specific host key. This made it easy for worms and other
malicious scripts to use this information and spread to other systems, once they had a single system compromised. To counter this,
the HashKnownHosts will hash each host, so it’s not readable anymore. While being unreadable for the human eye, it still allows
SSH to check for the next time you connect to the same system, as the results in the same hash.**
````bash

