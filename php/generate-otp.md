---
title: Script to Generate OTP
description: 
published: 1
date: 2022-07-02T05:45:25.974Z
tags: php, script, security, otp
editor: markdown
dateCreated: 2022-07-02T05:45:25.974Z
---

# Generate OTP using PHP

<br>

Examples of how to generate a Random OTP using PHP

<br>

## generateOTP() Function
````php
<?php
function generateOTP($n)
{
  $generator = "1357902468";
  $result = "";
  
  for ($i = 1; $i <= $n; $i++) {
    $result .= substr($generator, (rand() % (strlen($generator))), 1);
  }
  return $result;
}
$n = 6;
print_r(generateNumericOTP($n));
?>
````

### **generateRandom() Function**
````php
<?php
$n=10;
function generateRandom($n) {
    $characters = '0123456789abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ';
    $randomString = '';
  
    for ($i = 0; $i < $n; $i++) {
        $index = rand(0, strlen($characters) - 1);
        $randomString .= $characters[$index];
    }
  
    return $randomString;
}
  
echo getRandomString($n);
?>
````

### **Using random_bytes() function**
````php
<?php 
$n = 20;
$result = bin2hex(random_bytes($n));
echo $result;
?>
````