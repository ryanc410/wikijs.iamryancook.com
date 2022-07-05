---
title: Secure Apache with a Let's Encrypt SSL
description: 
published: 1
date: 2022-07-02T05:59:41.566Z
tags: security, ssl, lets-encrypt, apache, virtual-host
editor: markdown
dateCreated: 2022-07-02T05:59:41.566Z
---

# Secure Apache with a Let's Encrypt SSL

<br>

## Update Server and Install Certbot
````bash
sudo apt update
sudo apt install certbot
````

<br>

## Generate Strong Dh (Diffie-Hellman) Group
````bash
sudo openssl dhparam -out /etc/ssl/certs/dhparam.pem 2048
````

<br>

> To obtain an SSL certificate for the domain, we’re going to use the Webroot plugin that works by creating a temporary file for validating the requested domain in the ${webroot-path}/.well-known/acme-challenge directory. The Let’s Encrypt server makes HTTP requests to the temporary file to validate that the requested domain resolves to the server where certbot runs.
{.is-info}

<br>

## Create Directory Structure

<br>

To make it more simple we’re going to map all HTTP requests for .well-known/acme-challenge to a single directory, /var/lib/letsencrypt.
````bash
sudo mkdir -p /var/lib/letsencrypt/.well-known
sudo chgrp www-data /var/lib/letsencrypt
sudo chmod g+s /var/lib/letsencrypt
````

<br>

## letsencrypt.conf

<br>

Create this file and store it in `/etc/apache2/conf-available/`
````bash
Alias /.well-known/acme-challenge/ "/var/lib/letsencrypt/.well-known/acme-challenge/"
<Directory "/var/lib/letsencrypt/">
    AllowOverride None
    Options MultiViews Indexes SymLinksIfOwnerMatch IncludesNoExec
    Require method GET POST OPTIONS
</Directory>
````

<br>

## ssl-params.conf

<br>

Create this file and store it in `/etc/apache2/conf-available/`
````bash
SSLProtocol             all -SSLv3 -TLSv1 -TLSv1.1
SSLCipherSuite          ECDHE-ECDSA-AES128-GCM-SHA256:ECDHE-RSA-AES128-GCM-SHA256:ECDHE-ECDSA-AES256-GCM-SHA384:ECDHE-RSA-AES256-GCM-SHA384:ECDHE-ECDSA-CHACHA20-POLY1305:ECDHE-RSA-CHACHA20-POLY1305:DHE-RSA-AES128-GCM-SHA256:DHE-RSA-AES256-GCM-SHA384
SSLHonorCipherOrder     off
SSLSessionTickets       off

SSLUseStapling On
SSLStaplingCache "shmcb:logs/ssl_stapling(32768)"

Header always set Strict-Transport-Security "max-age=63072000; includeSubDomains; preload"
Header always set X-Frame-Options SAMEORIGIN
Header always set X-Content-Type-Options nosniff

SSLOpenSSLConfCmd DHParameters "/etc/ssl/certs/dhparam.pem"
````

<br>

## Enable apache modules
````bash
sudo a2enmod http2
sudo a2enmod ssl
sudo a2enmod headers
sudo a2enconf ssl-params 
sudo a2enconf letsencrypt
````

<br>

## Reload Apache
````bash
sudo systemctl reload apache2
````

<br>

## Run Certbot
````bash
sudo certbot certonly --agree-tos --email admin@example.com --webroot -w /var/lib/letsencrypt/ -d example.com -d www.example.com
````

<br>

## Virtual Host File
````bash
<VirtualHost *:80> 
  ServerName example.com
  ServerAlias www.example.com

  Redirect permanent / https://example.com/
</VirtualHost>

<VirtualHost *:443>
  ServerName example.com
  ServerAlias www.example.com

  Protocols h2 http/1.1

  <If "%{HTTP_HOST} == 'www.example.com'">
    Redirect permanent / https://example.com/
  </If>

  DocumentRoot /var/www/example.com/public_html
  ErrorLog ${APACHE_LOG_DIR}/example.com-error.log
  CustomLog ${APACHE_LOG_DIR}/example.com-access.log combined

  SSLEngine On
  SSLCertificateFile /etc/letsencrypt/live/example.com/fullchain.pem
  SSLCertificateKeyFile /etc/letsencrypt/live/example.com/privkey.pem

  # Other Apache Configuration

</VirtualHost>
````

<br>

## Reload Apache
````bash
sudo systemctl reload apache2
````