---
title: Usage Example
description: Bash Script Usage example function
published: true
date: 2022-07-19T18:45:47.150Z
tags: bash, cli, script, usage, --help, -h
editor: markdown
dateCreated: 2022-07-19T18:45:47.150Z
---

# Usage function for Bash Scripts
````bash
function usage()
{
    echo "$0 v1.0 (Date Created). Usage:"
    echo ""
    echo "command [-options] [arg1] [arg2] [arg3]"
    echo ""
    echo "Description of usage here."
    echo "-h    help"
    echo "-x    exit"
    echo "-l    blah"
    echo "-d    blah"
}
````