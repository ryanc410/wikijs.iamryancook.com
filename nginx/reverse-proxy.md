---
title: Using Nginx as a Reverse Proxy
description: How to configure Nginx as a reverse proxy
published: true
date: 2022-08-28T23:45:54.939Z
tags: nginx, reverse-proxy
editor: markdown
dateCreated: 2022-08-28T23:45:54.939Z
---

# How to Configure Nginx as a Reverse Proxy

<br>

## Install Nginx

<br>

````bash
sudo apt update
sudo apt install nginx -y
````

<br>

## Create a new Site Configuration

````bash
sudo nano /etc/nginx/sites-available/reverse_proxy
````

**reverse_proxy**

````bash
server {
	listen 80;
	root /var/www/example.com;

	index index.php index.html index.htm;

	server_name example.com;

	location / {
		try_files $uri $uri/ /index.php;
	}

	location ~ \.php$ {
		proxy_set_header X-Real-IP $remote_addr;
		proxy_set_header X-Forwarded-For $remote_addr;
		proxy_set_header Host $host;
		proxy_pass http://127.0.0.1:8080;
	}
	
  location ~* \.(js|css|jpg|jpeg|png|svg|html|htm)$ {
		expires 30d;
	}
	
  location ~ /\.ht {
		deny all;
	}
}
````

<br>

## Enable New Configuration

````bash
sudo ln -s /etc/nginx/sites-available/reverse_proxy /etc/nginx/sites-enabled/reverse_proxy
````

<br>

## Change Apache Settings

Change the Apache settings to listen on port 8080. 

````bash
sudo nano /etc/apache2/ports.conf
listen 127.0.0.1:8080
````

<br>

Also change the port inside any virtual host file you may have,

````bash
<VirtualHost 127.0.0.1:8080>
etc...
````


