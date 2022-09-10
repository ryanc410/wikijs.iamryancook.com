---
title: FileSystem Functions
description: PHP Built-in functions dealing with the file system
published: true
date: 2022-09-10T01:05:13.850Z
tags: functions, built-in, file-system
editor: markdown
dateCreated: 2022-09-10T01:05:13.850Z
---

# PHP FileSystem Functions

---

## basename

Returns the trailing name component when given a string containing the path to a file or directory.

**SYNTAX**
````php
basename(string $path, string $suffix = ""): string
````

---

## unlink

Deletes a file. Returns true on success and false on failure.

**SYNTAX**
````php
unlink(string $filename, ?resource $context = null): bool
````

---

## file_exists

Checks whether a file or directory exists.

**SYNTAX**
````php
file_exists(string $filename): bool
````

**EXAMPLE**
Tests whether a file exists
````php
<?php
$filename = '/path/to/foo.txt';

if (file_exists($filename)) {
    echo "The file $filename exists";
} else {
    echo "The file $filename does not exist";
}
?>

````

---

## is_readable

Checks whether a file exists and is readable.

**PHP May be accessing the file as your web server user(nobody, www-data)

**SYNTAX**
````php
is_readable(string $filename): bool
````

**EXAMPLE**
````php
<?php
$filename = 'test.txt';
if (is_readable($filename)) {
    echo 'The file is readable';
} else {
    echo 'The file is not readable';
}
?>

````

---

## mkdir
Makes a directory

**SYNTAX**
````php
 mkdir(
    string $directory,
    int $permissions = 0777,
    bool $recursive = false,
    ?resource $context = null
): bool
````

**EXAMPLE**
````php
<?php
mkdir("/path/to/my/dir", 0700);
?>
````


---

## is_uploaded_file

Tells whether the file was uploaded via POST

**SYNTAX**
````php
is_uploaded_file(string $filename): bool
````

For proper working, the function `is_uploaded_file()` needs an argument like `$_FILES['userfile']['tmp_name']`, - the name of the uploaded file on the client's machine `$_FILES['userfile']['name']` does not work.

**EXAMPLE**
````php
<?php

if (is_uploaded_file($_FILES['userfile']['tmp_name'])) {
   echo "File ". $_FILES['userfile']['name'] ." uploaded successfully.\n";
   echo "Displaying contents\n";
   readfile($_FILES['userfile']['tmp_name']);
} else {
   echo "Possible file upload attack: ";
   echo "filename '". $_FILES['userfile']['tmp_name'] . "'.";
}

?>
````

---

## move_uploaded_file
Moves an uploaded file to a new location

**SYNTAX**
````php
 move_uploaded_file(string $from, string $to): bool
 ````

 $from = The filename of the uploaded file 
 
 
 $to = The destination of the moved file

 > If from is not a valid upload file, then no action will occur, and move_uploaded_file() will return false. 

 > If from is a valid upload file, but cannot be moved for some reason, no action will occur, and move_uploaded_file() will return false. Additionally, a warning will be issued. 

 **EXAMPLE**
 ````php
<?php
$uploads_dir = '/uploads';
foreach ($_FILES["pictures"]["error"] as $key => $error) {
    if ($error == UPLOAD_ERR_OK) {
        $tmp_name = $_FILES["pictures"]["tmp_name"][$key];
        // basename() may prevent filesystem traversal attacks;
        // further validation/sanitation of the filename may be appropriate
        $name = basename($_FILES["pictures"]["name"][$key]);
        move_uploaded_file($tmp_name, "$uploads_dir/$name");
    }
}
?>
 ````