---
title: Bash Aliases
description: Useful Bash Aliases
published: true
date: 2022-07-10T02:40:00.213Z
tags: aliases, bash, cli
editor: markdown
dateCreated: 2022-07-09T16:23:36.910Z
---

# Useful Bash Aliases
````bash
alias c='clear'
alias s='sudo'

alias services='systemctl list-units  --type=service  --state=running'
alias listen='sudo netstat -ltup'

alias install="sudo apt install $1 -y"
alias web='cd /var/www/html'
alias vhosts='cd /etc/apache2/sites-available'
alias phpdir='cd /etc/php/*.*/'

alias passgen="openssl rand --base64 $1"
alias extract="tar -zxf $1.tar.gz"
alias encrypt="gpg -c $1"
````