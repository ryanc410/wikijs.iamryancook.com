---
title: Bash Aliases
description: Useful Bash Aliases
published: true
date: 2025-10-14T03:00:26.713Z
tags: bash, aliases, cli
editor: markdown
dateCreated: 2025-09-29T23:47:44.649Z
---

# Useful Bash Aliases
````bash
# Sets custom PS1
PS1='\[\e[0;31m\]\u@\h \[\e[0;36m\][\w]\$\[\e[0m\] '

# Clears the screen
alias c='clear'

# Sudo shortcut
alias s='sudo'

# List Running Services
alias services='systemctl list-units  --type=service  --state=running'

# List Services and the Ports theyre running on
alias listen='sudo netstat -ltup'

# Install shortcut
alias install="sudo apt install $1 -y"

# Navigate to WebRoot directory
alias web='cd /var/www/html'

# Navigate to Apache virtual hosts directory
alias vhosts='cd /etc/apache2/sites-available'

# Navigate to php config directory
alias phpdir='cd /etc/php/*.*/'

# Show Apache error log
alias checklog='cat /var/log/apache2/error.log'

# Restart Service
alias restart="sudo systemctl restart $1"

# Start Service
alias start="sudo systemctl start $1"

# Enable Service to run at boot
alias enable="sudo systemctl enable $1"

# Reload Service
alias reload="sudo systemctl reload $1"

# Check Service status
alias status="sudo systemctl status $1"

# Create password specified length
alias passgen="openssl rand --base64 $1"

# Extract TAR Archive
alias extract="tar -zxf $1.tar.gz"

# Encrypt 
alias encrypt="gpg -c $1"

# Decrypt
alias decrypt="gpg -d $1"

# Network tools
alias ipinfo='ip a'
alias ports='netstat -tulnp'
alias sniff='sudo tcpdump -i any'

# Recon shortcuts
alias nmapquick='nmap -T4 -F'
alias nmapfull='nmap -T4 -A -v'

# Metasploit
alias msf='msfconsole'

# Python webserver
alias serve='python3 -m http.server 8080'

alias listen='lsof -iTCP -sTCP:LISTEN -n -P +c0'

````
