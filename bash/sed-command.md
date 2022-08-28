---
title: Sed Command
description: How to use the Sed command in Bash
published: true
date: 2022-08-28T22:32:16.765Z
tags: bash, regex, regular-expressions, sed
editor: markdown
dateCreated: 2022-08-28T22:32:16.765Z
---

# SED

<br>

## Syntax

`sed 'command' filename`

<br>

## Metacharacter Functions

<br>

|---|---------------------------|
| `^` | Beginnning-of-line anchor |
| `$` | End of-line-anchor |
| `.` | Matches one character, but not the newline character |
| `*` | matches zero or more characters |
| `[]` | matches one character in the set |
| `[^ ]` | matches one character not in the set |
| `\(..\)` | This saves matched characters |
| `&` | This saves the search string so it can be remembered in the replacement string |
| `\<` | This is the beginning-of-word anchor |
| `\>` | This is the end-of-word anchor | 
| `x\{m\}` | This is the repetition of the character x:m times |
| `x\{m,\}` | This means at least m times |
| `x\{m,n\}` | This means between m and n times | 

<br>