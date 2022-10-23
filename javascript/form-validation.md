---
title: Form Validation (UNDER CONSTRUCTION)
description: Different examples of validating form elements using javascript
published: true
date: 2022-10-23T12:48:20.462Z
tags: forms, javascript, form-validation
editor: markdown
dateCreated: 2022-10-23T12:48:20.462Z
---

# Make sure the field isnt empty
````javascript
if(inputID.value.length == 0){
  document.getElementById("errorMsg").innerText = "All fields are mandatory!";
  inputID.focus();
  return false;
}
````

# Check for only Alphabetic Characters
````javascript
function inputAlpha(inputtext, alertMsg){
	var alphaExp = /^[a-zA-Z]+$/;
	if(inputtext.value.match(alphaExp)){
		return true;
	}else{
		document.getElementById('errorMsg').innerText = alertMsg;
		inputtext.focus();
		return false;
	}
}

// Usage
if (inputAlpha(inputfield, "Example Error message")){
 	return false; 
};
````


