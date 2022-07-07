---
title: Regular Expression Patterns
description: List of Patterns used to test matches on certain elements 
published: true
date: 2022-07-07T01:16:11.808Z
tags: form-validation, javascript, validation, regex, regular-expressions, tests
editor: markdown
dateCreated: 2022-07-07T01:16:11.808Z
---

# Match Email Address

**AUTHOR**: Ryan Cook
````javascript
^([a-zA-Z0-9_]{1,75})@{1}([a-zA-Z0-9]{1,50})\.{1}((\bcom\b)?(\bnet\b)?(\borg\b)?){1}$
````
                                                                     