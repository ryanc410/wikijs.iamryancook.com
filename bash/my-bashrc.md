---
title: Custom .bashrc File
description: 
published: true
date: 2022-10-18T05:08:44.563Z
tags: bash, custom, .bashrc
editor: markdown
dateCreated: 2022-09-10T22:06:59.881Z
---

# Custom .bashrc File

````bash
#      /$$                           /$$                          
#     | $$                          | $$                          
#     | $$$$$$$   /$$$$$$   /$$$$$$$| $$$$$$$   /$$$$$$   /$$$$$$$
#     | $$__  $$ |____  $$ /$$_____/| $$__  $$ /$$__  $$ /$$_____/
#     | $$  \ $$  /$$$$$$$|  $$$$$$ | $$  \ $$| $$  \__/| $$      
#     | $$  | $$ /$$__  $$ \____  $$| $$  | $$| $$      | $$      
#  /$$| $$$$$$$/|  $$$$$$$ /$$$$$$$/| $$  | $$| $$      |  $$$$$$$
# |__/|_______/  \_______/|_______/ |__/  |__/|__/       \_______/
                                                                

HISTSIZE=1000
HISTFILESIZE=2000
HISTCONTROL=ignoreboth

shopt -s histappend
shopt -s checkwinsize

# Directory Aliases
#---------------------------#
alias b1='cd ../'
alias b2='cd ../../'
alias b3='cd ../../../'
alias b4='cd ../../../../'
alias web='cd /var/www/html'
alias inc='cd /var/includes'
alias phpdir='cd /etc/php/*.*/apache2'
alias vhosts='cd /etc/apache2/sites-available'

# Command Aliases
#---------------------------#
alias s='sudo'
alias c='clear'
alias update="sudo apt update && sudo apt upgrade -y"
alias clean="sudo apt autoremove && sudo apt clean"
alias install="sudo apt install $1 -y"
alias genpass="openssl rand -base64 $1"
alias encrypt="gpg -c $1"
alias decrypt="gpg -d $1"
alias log="sudo tail /var/log/apache2/*-error.log"
alias checknet="sudo netstat -tlpn"
alias now='date +%b.%d.%Y-%I:%M%p'

# Program Aliases
#---------------------------#
alias reload="sudo systemctl reload $1"
alias restart="sudo systemctl restart $1"
alias enable="sudo systemctl enable $1"
alias start="sudo systemctl start $1"
alias stop="sudo systemctl stop $1"
alias status="sudo systemctl status $1"

alias ll='ls -alF'
alias la='ls -A'
alias l='ls -CF'
alias ls='ls --color=auto'
alias grep='grep --color=auto'
alias fgrep='fgrep --color=auto'
alias egrep='egrep --color=auto'

# Functions
#---------------------------#
# Extracts archive $1
function extract(){
    if [ -f $1 ] ; then
        case $1 in
            *.tar.bz2)   tar xvjf $1     ;;
            *.tar.gz)    tar xvzf $1     ;;
            *.bz2)       bunzip2 $1      ;;
            *.rar)       unrar x $1      ;;
            *.gz)        gunzip $1       ;;
            *.tar)       tar xvf $1      ;;
            *.tbz2)      tar xvjf $1     ;;
            *.tgz)       tar xvzf $1     ;;
            *.zip)       unzip $1        ;;
            *.Z)         uncompress $1   ;;
            *.7z)        7z x $1         ;;
            *)           echo "'$1' cannot be extracted via >extract<" ;;
        esac
    else
        echo "'$1' is not a valid file!"
    fi
}
# Displays $1 in Red
function error(){
      echo -e "\e[0;31m$1\e[0m"
}
# Displays $1 in Green
function success(){
    echo -e "\e[0;32m$1\e[0m\n"
}
# Checks to see if $1 is installed
function chk(){
    if [[ -z $1 ]]; then
	error "This function requires an argument!"
	sleep 3
	exit 1
    else
        dpkg -l | grep "$1" &>/dev/null && success "$1 PASS" || error "$1 FAIL"; apt install "$1" -y &>/dev/null
    fi
}

# Variables
#---------------------------#
export DOMAIN=$(hostname -f)
export month=$(date +%b)
export day=$(date +%d)
export year=$(date +%Y)
export time=$(date +%T%p)
export timestamp="${host}"_"${month}"."${day}"."${year}"-"${time}"

# Prompt
#---------------------------#

# Username@Hostname[Time]<Working Directory>
PS1='\[\e[0;96m\]\u\[\e[0;38;5;255m\]@\[\e[0;96m\]\H\[\e[0;97m\][\[\e[0;5;38;5;154m\]\@\[\e[0;97m\]]\[\e[0;94m\]<\[\e[0;38;5;154m\]\w\[\e[0;94m\]>\[\e[0m\]'

# Username@Hostname[IP Address]:(Working Directory)
# PS1='\[\e[0;92m\]\u\[\e[0;97m\]@\[\e[0;38;5;51m\]\H\[\e[0;91m\][\[\e[0;3m\]$(ip route get 1.1.1.1 | awk -F"src " '"'"'NR==1{split($2,a," ");print a[1]}'"'"')\[\e[0;91m\]]\[\e[0m\]:\[\e[0;91m\](\[\e[0m\]\W\[\e[0;91m\])\[\e[0m\]'

````