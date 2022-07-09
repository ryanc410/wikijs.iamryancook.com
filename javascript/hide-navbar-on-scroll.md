---
title: Hide Navbar on User scroll
description: 
published: true
date: 2022-07-09T12:36:26.249Z
tags: hide, how-to, javascript, navbar, scroll
editor: markdown
dateCreated: 2022-07-09T12:36:26.249Z
---

# Hide Navbar on User Scroll
````javascript
var prevScrollpos = window.pageYOffset;
window.onscroll = function() {
    var currentScrollPos = window.pageYOffset;
    if (prevScrollpos > currentScrollPos) {
        document.getElementById("navbar").style.top = "0";
    } else {
        document.getElementById("navbar").style.top = "-50px";
    }
    prevScrollpos = currentScrollPos;
} 
````