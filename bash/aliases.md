---
title: Bash Aliases
description: Useful Bash Aliases
published: true
date: 2022-07-18T02:41:57.102Z
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

alias checklog='cat /var/log/apache2/error.log"

alias restart="sudo systemctl restart $1"
alias start="sudo systemctl start $1"
alias enable="sudo systemctl enable $1"
alias reload="sudo systemctl reload $1"
alias status="sudo systemctl status $1"

alias passgen="openssl rand --base64 $1"
alias extract="tar -zxf $1.tar.gz"
alias encrypt="gpg -c $1"
````