---
title: Function to Get the Client's IP Address
description: 
published: 1
date: 2022-07-02T05:49:03.841Z
tags: php, script, security, ip-address
editor: markdown
dateCreated: 2022-07-02T05:49:03.841Z
---

# PHP Function to return Client's IP Address

<br>

````php
<?php

   function getRealIPAddr()
   {
       //check ip from share internet
       if (!empty($_SERVER['HTTP_CLIENT_IP'])) 
       {
           $ip = $_SERVER['HTTP_CLIENT_IP'];
       }
       //to check ip is pass from proxy
       elseif (!empty($_SERVER['HTTP_X_FORWARDED_FOR']))  
       {
           $ip = $_SERVER['HTTP_X_FORWARDED_FOR'];
       }
       else
       {
           $ip = $_SERVER['REMOTE_ADDR'];
       }

       return $ip;
   }

?>
````