---
title: Show/Hide using Jquery
description: 
published: 1
date: 2022-07-02T17:51:41.434Z
tags: jquery, show, hide, effects
editor: markdown
dateCreated: 2022-07-02T17:51:41.434Z
---

# Show and Hide Effects

<br>

## hide() Method

> The hide() method sets the inline style `display:none;` for selected elements. The show() method restores the display properties back to before the element was hidden.
{.is-info}

<br>

### Jquery Code
````javascript
$(document).ready(function(){
    // Hide displayed paragraphs
    $(".hide-btn").click(function(){
        $("p").hide();
    });
    
    // Show hidden paragraphs
    $(".show-btn").click(function(){
        $("p").show();
    });
});
````

<br>

### Specify Speed/Duration
````javascript
$(document).ready(function(){
    $(".hide-btn").click(function(){
        $("p.normal").hide();
        $("p.fast").hide("fast");
        $("p.slow").hide("slow");
        $("p.very-fast").hide(50);
        $("p.very-slow").hide(2000);
    });
});
````

<br>

### Callback Function

Display an alert message after hiding paragraphs
````javascript
$(document).ready(function(){
    $(".hide-btn").click(function(){
        $("p").hide("slow", function(){
            // Code to be executed
            alert("The hide effect is completed.");
        });
    });
````

<br>

## show()

<br>

### Specify the Speed to show
````javascript
    $(".show-btn").click(function(){
        $("p.normal").show();
        $("p.fast").show("fast");
        $("p.slow").show("slow");
        $("p.very-fast").show(50);
        $("p.very-slow").show(2000);
    });
});
````

<br>

### Callback Function that shows alert
````javascript
$(document).ready(function(){
    $(".show-btn").click(function(){
        $("p").show("slow", function(){
            // Code to be executed
            alert("The show effect is completed.");
        });
    });
});
````