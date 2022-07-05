---
title: Database Connection Script
description: 
published: 1
date: 2022-07-02T05:42:17.779Z
tags: php, mysqli_connect, database, mysql, script
editor: markdown
dateCreated: 2022-07-02T05:42:17.779Z
---

# Connect to A Mysql Database using PHP

<br>

## **db_connect.php**

````php
 <?php
$servername = "localhost";
$username = "username";
$password = "password";

// Create connection
$conn = mysqli_connect($servername, $username, $password);

// Check connection
if (!$conn) {
  die("Connection failed: " . mysqli_connect_error());
}
echo "Connected successfully";
?> 
````