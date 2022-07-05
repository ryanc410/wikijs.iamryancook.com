---
title: Toggle Method Examples
description: 
published: 1
date: 2022-07-02T17:53:49.102Z
tags: effects, jquery, toggle
editor: markdown
dateCreated: 2022-07-02T17:53:49.102Z
---

# Jquery Toggle Method

<br>

The jQuery toggle() method show or hide the elements in such a way that if the element is initially displayed, it will be hidden; if hidden, it will be displayed.

## **Toggles paragraphs display**
````javascript
$(document).ready(function(){
    $(".toggle-btn").click(function(){
        $("p").toggle();
    });
});
````

<br>

> You can specify the duration parameter for the toggle() method to make it animated like the show() and hide() methods.
{.is-info}


## **Toggles paragraphs at different speeds**
````javascript
$(document).ready(function(){
    $(".toggle-btn").click(function(){
        $("p.normal").toggle();
        $("p.fast").toggle("fast");
        $("p.slow").toggle("slow");
        $("p.very-fast").toggle(50);
        $("p.very-slow").toggle(2000);
    });
});
````

<br>

## **Callback functions**
````javascript
$(document).ready(function(){
    $(".toggle-btn").click(function(){
        $("p").toggle(1000, function(){
            // Code to be executed
            alert("The toggle effect is completed.");
        });
    });
});
````