---
title: How to Install Webmin on Ubuntu Server 20
description: 
published: 1
date: 2022-07-04T02:07:09.696Z
tags: how-to, ubuntu-server, webmin
editor: markdown
dateCreated: 2022-07-04T02:07:09.696Z
---

# Update Server packages

````bash
sudo apt update
````

# Add Webmin Repository

This command will add the Webmin Repository to your sources file.
````bash
echo "deb http://download.webmin.com/download/repository sarge contrib" | sudo tee -a /etc/apt/sources.list > /dev/null
````

# Download PGP Key and Add it to System

````bash
wget -q -O- http://www.webmin.com/jcameron-key.asc | sudo apt-key add
````

# Update and Install

````bash
sudo apt update && sudo apt install webmin -y
````

# Install Script

````bash
#!/usr/bin/env bash

sudo apt update &>/dev/null
echo "deb http://download.webmin.com/download/repository sarge contrib" | sudo tee -a /etc/apt/sources.list > /dev/null

wget -q -O- http://www.webmin.com/jcameron-key.asc | sudo apt-key add
sudo apt update && sudo apt install webmin -y
````