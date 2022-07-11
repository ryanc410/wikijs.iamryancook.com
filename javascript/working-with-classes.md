---
title: Working with Classes in Javascript
description: 
published: true
date: 2022-07-11T01:34:34.831Z
tags: classes, classlist, classname, hasclass, javascript
editor: markdown
dateCreated: 2022-07-05T06:37:44.357Z
---

# Selecting Elements by Class Name

<br>

**SYNTAX**

Returns all elements with class "example" in an array like HTML collection.
````javascript
const el = document.getElementsByClassName("example");
````

## Accessing Class Elements

The elements in a HTML collection can be accessed by index starting at [0].

**EXAMPLE**
````html
<div class="class1"><h1>Class 1</h1></div>
<div class="class1"><h2>Class 1 too</h2></div>

# Selects the second class1 element
const el = document.getElementsByClassName("class1")[1];
````

<br>

# Check if an Element Contains a Specific Class

<br>

## Syntax

<br>

````javascript
element.classList.contains(CLASSNAME);
````

## Example

<br>

````html
<div class="myClass">Element</div>
<script>
  const div = document.querySelector('div');
  div.classList.contains('myClass');
</script>
````

The previous example returns true because the classname 'myClass' is present on the div element.

<br>

# Add a Class Name to an Element

<br>

## className() Property

> The className property of the Element interface is used for getting and setting the value of the given element's class attribute.
{.is-info}

<br>

### Example #1

<br>

````javascript
document.querySelector('ELEMENT_CLASS').className = 'NEW_CLASS_NAME';
````

<br>


### Example #2

<br>

````html
    <div id="divId" class="someClass ">
      <p>Add new classes</p>
    </div>
    <script>
      let cName = document.getElementById("divId");
      cName.className += "otherClass";
      alert(cName.className);
    </script>
````

<br>

> It’s important to include the space after “someclass”, otherwise it compromises the existing classes coming before it in the class list.
{.is-warning}

<br>

### Example Using onclick inside HTML

<br>

**ADD an onclick event listener to the button in html**

````html
 <button class="oldClassName" id="buttonId" onclick="changeClass()">Click on Button</button>
````

````javascript
      function changeClass() {
        document.getElementById('buttonId').className = "newClassName";
        let button_class = document.getElementById('buttonId').className;
      }
````

<br>

### Example Using addEventListener()

<br>

````javascript
 function changeClass() {
        document.getElementById('buttonId').className = "newClassName";
        let button_class = document.getElementById('buttonId').className;
      }
      window.onload = function() {
        document.getElementById("buttonId").addEventListener('click', changeClass);
      }
````

<br>

## add() Method

<br>

### Example #1

````javascript
document.querySelector('ELEMENT_CLASS').classList.add('NEW_CLASSNAME');
````

<br>

### Example #2

<br>

````javascript
function addClass() {
        let cName = document.getElementById("divId");
        cName.classList.add("addNewClass");
}
````

# Toggle Class of an Element

<br>

## Syntax

````javascript
var el = document.getElementById('ELEMENT_ID');

el.classList.toggle('className');
````

<br>

## Example

<br>

**HTML**
````html
<div class="show">Item</div>
````

**JAVASCRIPT**

````javascript
const div = document.querySelector('div');
div.classList.toggle('show');
````