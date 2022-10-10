---
title: PHP Mail Test Script
description: Tests the server's ability to send email using PHP's built in mail function.
published: true
date: 2022-10-10T14:29:41.454Z
tags: php, email, mail-test
editor: markdown
dateCreated: 2022-08-28T15:42:10.985Z
---

# PHP Mail Test Script

> Use this script to test PHP's built in mail functionality. 
{.is-info}

**In order to use,** 
1. Simply copy this script to a new file on the machine. 
2. Change the $from, $to, $subject, $message values to your own values.
3. Run the script by executing `php scriptname.php`
4. Check your email to see if you received it.

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