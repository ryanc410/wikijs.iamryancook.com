---
title: Adding Event Listeners to HTML Elements
description: 
published: 1
date: 2022-07-02T04:06:07.117Z
tags: how-to, javascript, web-development
editor: markdown
dateCreated: 2022-07-02T04:06:07.117Z
---

# Basic Syntax

````javascript
document.addEventListener("click", myFunction);

function myFunction() {
  document.getElementById("demo").innerHTML = "Hello World";
}
````

## Simple Version of the Same Code

````javascript
document.addEventListener("click", function(){
  document.getElementById("demo").innerHTML = "Hello World";
}); 
````

# Add Multiple Event Listeners to the Document
````javascript
document.addEventListener("click", myFunction1);
document.addEventListener("click", myFunction2); 
````

# Add Different Types of Events
````javascript
document.addEventListener("mouseover", myFunction);
document.addEventListener("click", someOtherFunction);
document.addEventListener("mouseout", someOtherFunction); 
````

# Use an Anonymous function to pass parameters
````javascript
document.addEventListener("click", function() {
  myFunction(p1, p2);
}); 
````

# Change the Background Color of the Page
````javascript
document.addEventListener("click", function(){
  document.body.style.backgroundColor = "red";
}); 
````
