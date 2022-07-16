---
title: Bash Backup Script
description: Backup script that takes the files/directories provided as arguments to the script and archives them
published: true
date: 2022-07-16T13:03:29.340Z
tags: bash, script, backup
editor: markdown
dateCreated: 2022-07-16T13:03:29.340Z
---

# bash_backup.sh
````bash
#!/usr/bin/env bash
#############################################################
# Script Name: backup.sh
# Author: Ryan C
# Date Modified: 07/16/2022
#############################################################
backup_dirs="$@"
list=backup_list.txt
backup_destination=/home/backups/
backup_time=$(date +%T%p)
log=$(ls -R1 $backup_dirs)

host_name=$(hostname -f)
month=$(date +%b)
day=$(date +%e)
year=$(date +%Y)
archivename="${host_name}_${month}.${day}.${year}".tar.gz

function error(){
    echo -e "\e[1;31m$1\e[0m\n"
}
function success(){
    echo -e "\e[1;32m$1\e[0m\n"
}

if [[ $EUID -ne -0 ]]; then
    clear
    error "Script must be ran as root!"
    sleep 3
    exit 1
fi

if [[ $# -eq 0 ]]; then
    error "Script was executed without specifying what to backup"
    sleep 3
    exit 1
fi

if [[ ! -d $backup_destination ]]; then
    mkdir -p "$backup_destination" &>/dev/null
fi

printf "%s\n" "${backup_dirs[@]}">>"$list"
while read -r dirs
do
    if [[ ! -d $dirs ]]; then
        error "Could not find $dirs on system.."
        sleep 3
        exit 3
    fi
done < "$list"

tar -czf "$archivename" -T "$list" &>/dev/null

mv "$archivename" "$backup_destination"

rm -rf "$list"

if [[ ! -f $backup_destination/$archivename ]]; then
    error "Backup Failed!"
    sleep 3
    exit 4
else
    success "Backup Completed!"
    sleep 3
fi

find "$backup_destination" -mindepth 1 -mtime +7 -delete

cat << _EOF_ > "$backup_destination"/backuplog_"$backup_time".txt
############################
BACKUP COMPLETED SUCCESSFULLY!
############################

$month $day, $year @ $backup_time

#############################
DIRECTORIES AND FILES BACKED UP
#############################
$log
_EOF_

exit 0
````