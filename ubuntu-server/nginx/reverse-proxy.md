---
title: Nginx Reverse Proxy for Apache
description: 
published: 1
date: 2022-07-05T04:17:41.163Z
tags: apache, how-to, reverse-proxy, webserver, nginx
editor: markdown
dateCreated: 2022-07-05T04:17:41.163Z
---

# Install Apache Web Server

IF you dont have Apache installed already, install it using:

````bash
sudo apt install apache2 apache2-utils -y
````

# Change Apache Listen Port

In order to have both Apache and Nginx functioning, you must change the Apache Listen Port. You can change it to whatever but the recommended port to change it to is 8080.

````bash
cd /etc/apache2
mv ports.conf ports.conf.original
echo "Listen 8080">ports.conf
````

# Start and Enable Apache

````bash
sudo systemctl start apache2
sudo systemctl enable apache2
````

# Install Nginx

````bash
sudo apt-get install nginx -y
````

# Create Proxy Configuration

**/etc/nginx/conf.d/proxy.conf**
````bash
server {
listen 80;
server_name test.example.com;
location ~ .php$ {
proxy_pass http://SERVERIPADDRESS:8080;
proxy_set_header Host $host;
proxy_set_header X-Real-IP $remote_addr;
proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
proxy_set_header X-Forwarded-Proto $scheme;
}
}
````