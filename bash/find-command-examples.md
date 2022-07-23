---
title: Find Command Examples
description: Different ways to use the find command when searching for files in Bash
published: true
date: 2022-07-23T15:40:42.144Z
tags: bash, cli, examples, find
editor: markdown
dateCreated: 2022-07-23T15:40:42.144Z
---

# Files by name (Non-case sensitive)
````bash
find /path/to/search -name '*.txt' -print
````

<br>

# Logical Operators (or & and)

**Or**
````bash
find . \( -name '*.txt' -o -name '*.pdf' \) -print
````

**And**
````bash
find . \( -name '*e*' -and -name 's*' \) 
````

<br>

# Using Regular Expressions
**Match .py or .sh files in current directory**
````bash
find . -regex '.*\.(py\|sh\)$'
````

**Case insensitive**
````bash
find . -iregex '.*\(\.py\|\.sh\)$'
````

<br>

# Finding files that dont match a pattern
**Find all files that do not end in .txt**
````bash
find . ! -name "*.txt" -print
````

<br>

# Finding files using Mindepth
**Find files that are atleast 2 subdirectories distant from current Directory**
````bash
find . -mindepth 2 -name "f*" -print
````

<br>

# By File Type

**Directories**
````bash
find . -type d -print
````

**Files**
````bash
find . -type f -print
````

**Symbolic Links**
````bash
find . -type l -print
````

# By Timestamps
**Files accessed within past 7 days**
````bash
find . -type f -atime -7 -print
````

**Print files that have an access time exactly seven days old**
````bash
find . -type f -atime 7 -print
````

**Print files that have an access time older than seven days**
````bash
find . -type f -atime +7 -print
````

**Print all the files that have an access time older than seven minutes**
````bash
find . -type f -amin +7 -print
````

**Find all the files that were modified more recently than file.txt**
````bash
find . -type f -newer file.txt -print
````