---
title: Bash Loops
description: 
published: true
date: 2022-07-19T18:51:17.294Z
tags: bash, cli, loops, scripting
editor: markdown
dateCreated: 2022-07-19T18:51:17.294Z
---

# Bash Loops

<br>

## Read a file line by line.

````bash
#!/bin/bash
FILE=$1
# read $FILE using the file descriptors
exec 3<&0
exec 0<$FILE
while read line
do
	# use $line variable to process line
	echo $line
done
exec 0<&3
````

## Evaluate options passed on Command Line
````bash
while getopts ae:f:hd:s:qx: option
do
        case "${option}"
        in
                a) ALARM="TRUE";;
                e) ADMIN=${OPTARG};;
                d) DOMAIN=${OPTARG};;
                f) SERVERFILE=$OPTARG;;
                s) WHOIS_SERVER=$OPTARG;;
                q) QUIET="TRUE";;
                x) WARNDAYS=$OPTARG;;
                \?) usage
                    exit 1;;
        esac
done
````

## Read input from a file
````bash
#!/bin/bash
 
# Script name: block_ips.sh
 
# Set the Internal Field Separator to an octothorpe '#'
IFS='#'
 
# Set input file name here
INPUT="bad-guys.ips.txt"
 
# Read file line-by-line to get an IP and comment to block it using the iptables 
while read -r ip comment
do
	/sbin/iptables -A INPUT -s "$ip" -m comment --comment "$comment" -j DROP
 
done < "$INPUT"
````


### Conditional While loop exit with Break Statement
````bash
while [ condition ]
do
   statements1      #Executed as long as condition is true and/or, up to a disaster-condition if any.
   statements2
  if (disaster-condition)
  then
	break       	   #Abandon the while lopp.
  fi
  statements3          #While good and, no disaster-condition.
done
````
