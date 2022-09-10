---
title: Custom .bashrc File
description: 
published: true
date: 2022-09-10T22:06:59.881Z
tags: bash, custom, .bashrc
editor: markdown
dateCreated: 2022-09-10T22:06:59.881Z
---

# Custom .bashrc File

````bash
# ~/.bashrc: executed by bash(1) for non-login shells.
# see /usr/share/doc/bash/examples/startup-files (in the package bash-doc)
# for examples

# If not running interactively, don't do anything
case $- in
    *i*) ;;
      *) return;;
esac

# don't put duplicate lines or lines starting with space in the history.
# See bash(1) for more options
HISTCONTROL=ignoreboth

# append to the history file, don't overwrite it
shopt -s histappend

# for setting history length see HISTSIZE and HISTFILESIZE in bash(1)
HISTSIZE=1000
HISTFILESIZE=2000

# check the window size after each command and, if necessary,
# update the values of LINES and COLUMNS.
shopt -s checkwinsize

# If set, the pattern "**" used in a pathname expansion context will
# match all files and zero or more directories and subdirectories.
#shopt -s globstar

# make less more friendly for non-text input files, see lesspipe(1)
[ -x /usr/bin/lesspipe ] && eval "$(SHELL=/bin/sh lesspipe)"

# set variable identifying the chroot you work in (used in the prompt below)
if [ -z "${debian_chroot:-}" ] && [ -r /etc/debian_chroot ]; then
    debian_chroot=$(cat /etc/debian_chroot)
fi

# enable color support of ls and also add handy aliases
if [ -x /usr/bin/dircolors ]; then
    test -r ~/.dircolors && eval "$(dircolors -b ~/.dircolors)" || eval "$(dircolors -b)"
    alias ls='ls --color=auto'
    #alias dir='dir --color=auto'
    #alias vdir='vdir --color=auto'

    alias grep='grep --color=auto'
    alias fgrep='fgrep --color=auto'
    alias egrep='egrep --color=auto'
fi

# colored GCC warnings and errors
#export GCC_COLORS='error=01;31:warning=01;35:note=01;36:caret=01;32:locus=01:quote=01'

# some more ls aliases
alias ll='ls -alF'
alias la='ls -A'
alias l='ls -CF'

# Add an "alert" alias for long running commands.  Use like so:
#   sleep 10; alert
alias alert='notify-send --urgency=low -i "$([ $? = 0 ] && echo terminal || echo error)" "$(history|tail -n1|sed -e '\''s/^\s*[0-9]\+\s*//;s/[;&|]\s*alert$//'\'')"'

# Alias definitions.


# enable programmable completion features (you don't need to enable
# this, if it's already enabled in /etc/bash.bashrc and /etc/profile
# sources /etc/bash.bashrc).
if ! shopt -oq posix; then
  if [ -f /usr/share/bash-completion/bash_completion ]; then
    . /usr/share/bash-completion/bash_completion
  elif [ -f /etc/bash_completion ]; then
    . /etc/bash_completion
  fi
fi

##############################
# USER ALIASES
##############################

alias s='sudo'
alias c='clear'
alias update="sudo apt update && sudo apt upgrade -y"
alias clean="sudo apt autoremove && sudo apt clean"
alias b1='cd ../'
alias b2='cd ../../'
alias b3='cd ../../../'
alias b4='cd ../../../../'

alias install="sudo apt install $1 -y"
alias reload="sudo systemctl reload $1"
alias restart="sudo systemctl restart $1"
alias enable="sudo systemctl enable $1"
alias start="sudo systemctl start $1"
alias stop="sudo systemctl stop $1"
alias status="sudo systemctl status $1"

alias web='cd /var/www/html'
alias inc='cd /var/includes'
alias phpdir='cd /etc/php/*.*/apache2'
alias vhosts='cd /etc/apache2/sites-available'

alias chklog="sudo tail /var/log/apache2/713techsupport.com-error.log"
alias chknet="sudo netstat -tlpn"
alias now='date +%b.%d.%Y-%I:%M%p'
alias genpass="openssl rand -base64 $1"

alias extract="tar -xf $1.tar.gz"
alias encrypt="gpg -c $1"
alias decrypt="gpg -d $1"

##############################
# USER VARIABLES
##############################

export DOMAIN=$(hostname -f)
export IP=$(ifconfig | grep -Eo 'inet (addr:)?([0-9]*\.){3}[0-9]*' | grep -Eo '([0-9]*\.){3}[0-9]*' | grep -v '127.0.0.1')
export month=$(date +%b)
export day=$(date +%d)
export year=$(date +%Y)
export time=$(date +%T%p)
export timestamp="${host}"_"${month}"."${day}"."${year}"-"${time}"

PS1='\[\e[0;96m\]\u\[\e[0;38;5;255m\]@\[\e[0;96m\]\H\[\e[0;97m\][\[\e[0;5;38;5;154m\]\@\[\e[0;97m\]]\[\e[0;94m\]<\[\e[0;38;5;154m\]\w\[\e[0;94m\]>\[\e[0m\]'

##############################
# USER FUNCTIONS
##############################

function error(){
      echo -e "\e[0;31m$1\e[0m"
}
function success(){
    echo -e "\e[0;32m$1\e[0m\n"
}
function chk(){
    if [[ -z $1 ]]; then
	error "This function requires an argument!"
	sleep 3
	exit 1
    else
        dpkg -l | grep "$1" &>/dev/null && success "$1 PASS" || error "$1 FAIL"; apt install "$1" -y &>/dev/null
    fi
}


````