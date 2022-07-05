---
title: Custom BASH Functions
description: Custom BASH functions written by me to make things easier
published: 1
date: 2022-07-02T11:18:27.826Z
tags: bash, cli, functions
editor: markdown
dateCreated: 2022-07-02T03:20:53.020Z
---

# goto() Function

<br>

````bash
function goto(){
	while [[ ! -z $1 ]]; do
  case "$1" in
  	web|WEB|webroot|Webroot)		shift
    														cd /var/www/html;;
		php|PHP|phpdir|PHPDIR)			shift
    														cd /etc/php/*.*/;;
    inc|INC|includes|INCLUDES)	shift
    														cd /var/includes;;
    logs|LOGS|log|LOG)					shift
    														cd /var/log/apache2;;
    *)													echo -e "\e[1;31mUnrecognized Input\e[0m"
    														sleep 3
                                break;;
	esac
  shift
  done
}
````

<br>

# app() Function

<br>

````bash
function app(){
	while [[ ! -z $1 ]]; do
  	case "$1" in
    	restart)		shift
      						sudo systemctl restart "$1";;
      enable)			shift
      						sudo systemctl enable "$1";;
      start)			shift
      						sudo systemctl start "$1";;
      status)			shift
      						sudo systemctl status "$1";;
      *)					shift
      						echo -e "\e[1;31mUnrecognized Input\e[0m"
                  sleep 3
                  break;;
    esac
done
}
````
