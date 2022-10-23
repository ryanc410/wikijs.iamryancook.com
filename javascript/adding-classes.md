---
title: How to Add a Class to an Element
description: Different ways to add a CSS Class to an element using Javascript
published: true
date: 2022-10-23T12:35:49.574Z
tags: javascript, classlist, classname
editor: markdown
dateCreated: 2022-10-23T12:35:49.574Z
---

# .className Property

> Used for getting and setting the value of the given element's class attribute.
{.is-info}

Add an ID to an element for easy reference, and store as variable.
````html
<div id="elem1" class="someClass"></div>
````

Then use the .className property to add a class
````javascript
let elem = document.getElementById("elem1");
elem.className += "otherClass";
````

# .add Method

````javascript
function addClass() {
	let elem = document.getElementById("elem1");
	elem.classList.add("addNewClass");
	alert(elem.classList);
}
	addClass();
````