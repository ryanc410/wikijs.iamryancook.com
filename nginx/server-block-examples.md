---
title: Server Block Examples for Nginx
description: 
published: true
date: 2022-07-09T16:57:21.470Z
tags: nginx, virtual-host, webserver, server-blocks
editor: markdown
dateCreated: 2022-07-09T16:57:21.470Z
---

# Two Server Blocks, Serving Static Files
````bash
http {
  index index.html;

  server {
    server_name www.domain1.com;
    access_log logs/domain1.access.log main;

    root /var/www/domain1.com/htdocs;
  }

  server {
    server_name www.domain2.com;
    access_log  logs/domain2.access.log main;

    root /var/www/domain2.com/htdocs;
  }
}
````

# Catch All Server Block
````bash
http {
  index index.html;

  server {
    listen 80 default_server;
    server_name _; # This is just an invalid value which will never trigger on a real hostname.
    access_log logs/default.access.log main;

    server_name_in_redirect off;

    root  /var/www/default/htdocs;
  }
}
````

# Wildcard Subdomains in Parent Folder
````bash
server {
  # Replace this port with the right one for your requirements
  listen 80 default_server;  #could also be 1.2.3.4:80

  # Multiple hostnames separated by spaces.  Replace these as well.
  server_name star.yourdomain.com *.yourdomain.com; # Alternately: _

  root /PATH/TO/WEBROOT;

  error_page 404 errors/404.html;
  access_log logs/star.yourdomain.com.access.log;

  index index.php index.html index.htm;

  # static file 404's aren't logged and expires header is set to maximum age
  location ~* \.(jpg|jpeg|gif|css|png|js|ico|html)$ {
    access_log off;
    expires max;
  }

  location ~ \.php$ {
    include fastcgi_params;
    fastcgi_intercept_errors on;
    # By all means use a different server for the fcgi processes if you need to
    fastcgi_pass   127.0.0.1:YOURFCGIPORTHERE;
  }

  location ~ /\.ht {
    deny  all;
  }
}
````