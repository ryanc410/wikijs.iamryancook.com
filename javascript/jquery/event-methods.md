---
title: Commonly Used Event Methods
description: 
published: 1
date: 2022-07-02T11:23:28.657Z
tags: jquery, event-methods
editor: markdown
dateCreated: 2022-07-02T11:23:28.657Z
---

# Examples of Commonly Used Event Methods

<br>

# **click()**
````javascript
$("p").click(function(){
    $(this).hide();
});
````
# **dblclick()**
````javascript
$("p").dblclick(function(){
    $(this).hide();
});
````
# **mouseenter()**
````javascript
$("#p1").mouseenter(function(){
    alert("You entered p1!");
});
````
# **mouseleave()**
````javascript
$("#p1").mouseleave(function(){
    alert("Bye! You now leave p1!");
});
````
# **mousedown()**
````javascript
$("#p1").mousedown(function(){
    alert("Mouse down over p1!");
});
````
# **mouseup()**
````javascript
$("#p1").mouseup(function(){
    alert("Mouse up over p1!");
});
````
# **hover()**
````javascript
$("#p1").hover(function(){
        alert("You entered p1!");
    },
    function(){
        alert("Bye! You now leave p1!");
    });
````
# **focus()**
````javascript
$("input").focus(function(){
    $(this).css("background-color", "#cccccc");
});
````
# **blur()**
````javascript
$("input").blur(function(){
    $(this).css("background-color", "#ffffff");
});
````
# **on()**
Atttaches one or more event handlers for the selected elements.
````javascript
$("p").on("click", function(){
    $(this).hide();
});
````

````javascript
$("p").on({
    mouseenter: function(){
        $(this).css("background-color", "lightgray");
    },
    mouseleave: function(){
        $(this).css("background-color", "lightblue");
    },
    click: function(){
        $(this).css("background-color", "yellow");
    }
});
````