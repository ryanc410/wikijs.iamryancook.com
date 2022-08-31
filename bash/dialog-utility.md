---
title: Dialog Utility
description: Using the dialog utility in bash scripts
published: true
date: 2022-08-31T04:52:34.214Z
tags: bash, scripting, dialog, utility
editor: markdown
dateCreated: 2022-08-31T04:52:34.214Z
---

# Installation

<br>

````bash
sudo apt update
sudo apt install dialog
````

<br>

**Create A configuration file**

````bash
dialog --create-rc ~/.dialogrc
````

<br>

# Syntax

<br>

````bash
dialog --common-options --boxType "Text" Height Width --box-specific-option
````

<br>

> `common-options` is used to set the background-color, title etc.
{.is-info}

<br>

# Message Box (msgbox)

<br>

````bash
dialog --msgbox "This is a message." 10 50
````

## Message Box with Title

<br>

````bash
dialog --title "Hello" --msgbox 'Hello world!' 6 20
````

<br>

**Broken Down**
`--title "Hello"`: Set the Title of the box as Hello

<br>

`--msgbox "Hello World"`: The content of the message box

<br>

`6`: Set the height of the box

<br>

`20`:Set the width

# Yes/No box (yesno)

<br>

````bash
dialog --yesno "Would you like to continue?" 10 50
````

**With a Title**

````bash
dialog --title "yesno box" --yesno "Would you like to continue?" 10 50
````

**Inside a Shell Script**

````bash
#!/bin/bash
dialog --title "Delete file" \
--backtitle "Learning Dialog Yes-No box" \
--yesno "Do you want to delete file \"~/work/sample.txt\"?" 7 60
# Selecting "Yes" button will return 0.
# Selecting "No" button will return 1.
# Selecting [Esc] will return 255.
result=$?
case $result in
0) rm ~/work/sample.txt
echo "File deleted.";;
1) echo "File could not be deleted.";;
255) echo "Action Cancelled – Presssed [ESC] key.";;
esac
````

<br>

# Input Box (inputbox)

<br>

````bash
dialog --inputbox "Please enter something." 10 50 \
2> /tmp/tempfile
VAR=`cat ~/work/output.txt
````

**Inside a Script**

<br>

````bash
#!/bin/bash
result="output.txt"
>$ $result # Create empty file
dialog --title "Inputbox Demo" \
--backtitle "Learn Shell Scripting" \
--inputbox "Please enter your name " 8 60 2>$result
response=$?
name=$(<$result)
case $response in
0) echo "Hello $name"
;;
1) echo "Cancelled."
;;
255) echo "Escape key pressed."
esac
rm $result
````

<br>

# Textbox (textbox)

<br>

````bash
dialog --textbox /etc/passwd 10 50
````

<br>

# Password Box 

<br>

````bash
#!/bin/bash
# creating the file to store password
result="output.txt 2>/dev/null"
# delete the password stored file, if program is exited pre-maturely.
trap "rm -f output.txt" 2 15
dialog --title "Password" \
--insecure \
--clear \
--passwordbox "Please enter password" 10 30 2> $result
reply=$?
case $reply in
0) echo "You have entered Password : $(cat $result)";;
1) echo "You have pressed Cancel";;
255) cat $data && [ -s $data ] || echo "Escape key is pressed.";;
esac
````

<br>

# Menu Box

<br>

````bash
#!/bin/bash
# Declare file to store selected menu option
RESPONSE=menu.txt
# Declare file to store content to display date and cal output
TEMP_DATA=output.txt
vi_editor=vi
# trap and delete temp files
trap "rm $TEMP_DATA; rm $RESPONSE; exit" SIGHUP SIGINT SIGTERM
function display_output(){
dialog --backtitle "Learning Shell Scripting" --title "Output" --clear --msgbox
"$(<$TEMP_DATA)" 10 41
}
function display_date(){
echo "Today is `date` @ $(hostname -f)." >$TEMP_DATA
display_output 6 60 "Date and Time"
}
function display_calendar(){
cal >$TEMP_DATA
display_output 13 25 "Calendar"
}
# We are calling infinite loop here
while true
do
# Show main menu
dialog --help-button --clear --backtitle "Learn Shell Scripting" \
--title "[ Demo Menubox ]" \
--menu "Please use up/down arrow keys, number keys\n\
1,2,3.., or the first character of choice\n\
as hot key to select an option" 15 50 4 \
Calendar "Show the Calendar" \
Date/time "Show date and time" \
Editor "Start vi editor" \
Exit "Terminate the Script" 2>"${RESPONSE}"
menuitem=$(<"${RESPONSE}")
# Start activity as per selected choice
case $menuitem in
Calendar) display_calendar;;
Date/time) display_date;;
Editor) $vi_editor;;
Exit) echo "Thank you !"; break;;
esac
done
# Delete temporary files
[ -f $TEMP_DATA ] && rm $TEMP_DATA
[ -f $RESPONSE ] && rm $RESPONSE
````

<br>

# Checklist Box

<br>

````bash
dialog --checklist "This is a checklist" 10 50 2 \
"a" "This is one option" "off" \
"b" "This is the second option" "on"
````

<br>

**Select only one option**

<br>

````bash
dialog --radiolist "This is a selective list, where only one \
option can be chosen" 10 50 2 \
"a" "This is the first option" "off" \
"b" "This is the second option" "on"
````