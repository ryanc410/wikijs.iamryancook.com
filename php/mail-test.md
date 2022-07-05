---
title: PHP Mail Test Script
description: Tests the server's ability to send email using PHP's built in mail function.
published: 1
date: 2022-06-30T11:41:23.362Z
tags: php, email, mail-test
editor: markdown
dateCreated: 2022-06-30T11:41:19.266Z
---

# PHP Mail Test Script

````php
<?php 
	ini_set( 'display_errors', 1 );
  error_reporting( E_ALL );
  $from = "";
  $to = "";
  $subject = "PHP Mail Test script";
  $message = "This is a test to check the PHP Mail functionality";
  $headers = "From:" . $from;
  mail($to,$subject,$message, $headers);
  echo "Test email sent";
?>
````