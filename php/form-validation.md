---
title: Input Field Validation Using PHP
description: 
published: 1
date: 2022-07-02T05:47:15.907Z
tags: forms, php, security, validation, form-validation
editor: markdown
dateCreated: 2022-07-02T05:47:15.907Z
---

# Form Validation using PHP

<br>

### **Validate Name**
````php
$name = test_input($_POST["name"]);
if (!preg_match("/^[a-zA-Z-' ]*$/",$name)) {
  $nameErr = "Only letters and white space allowed";
}
````

<br>

### **Validate Email Using filter_var()**
````php
$email = test_input($_POST["email"]);
if (!filter_var($email, FILTER_VALIDATE_EMAIL)) {
  $emailErr = "Invalid email format";
}
````

<br>

### Using preg_match()
````php
<?php

   $email = "some@email.com";
   $pattern = "~([a-zA-Z0-9!#$%&'*+-/=?^_`{|}~])@([a-zA-Z0-9-]).([a-zA-Z0-9]{2,4})~";

   if(preg_match($pattern, $email))
   {
       echo 'This is a valid email.';
   }
   else
   {
       echo 'This is an invalid email.';
   }
?>
````

<br>

### **Validate URL**
````php
$website = test_input($_POST["website"]);
if (!preg_match("/\b(?:(?:https?|ftp):\/\/|www\.)[-a-z0-9+&@#\/%?=~_|!:,.;]*[-a-z0-9+&@#\/%=~_|]/i",$website)) {
  $websiteErr = "Invalid URL";
}
````

<br>

### **PHP Function to Sanitize User Input**
````php
function test_input($data) {
  $data = trim($data);
  $data = stripslashes($data);
  $data = htmlspecialchars($data);
  return $data;
}
````