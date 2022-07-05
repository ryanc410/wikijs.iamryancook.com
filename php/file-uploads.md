---
title: Handling File Uploads with PHP
description: 
published: 1
date: 2022-07-02T03:37:22.730Z
tags: php, file-uploads, forms
editor: markdown
dateCreated: 2022-07-01T02:32:25.579Z
---

# Adding File Upload Field to a Form
> In order for a form to be able to handle file uploads, the form tag must have the enctype attribute set. See the example below..
{.is-info}

````html
<form action="" method="post" enctype="multipart/form-data">
````

After you have this set, you can add a file input field like the one below:
````html
<input type="file" name="image" id="image">
````

# $_FILES array

The $_FILES array contains alot of useful information when handling file uploads.

**The original name of the uploaded file**
`$_FILES['INPUT_FIELD_NAME']['name']`

**Uploaded file's MIME Type**
`$_FILES['INPUT_FIELD_NAME']['type']`

**Location of the uploaded file**
`$_FILES['INPUT_FIELD_NAME']['tmp_name']`

**Integer indicating status of the upload**
`$_FILES['INPUT_FIELD_NAME']['error']`

**Size of uploaded file in bytes**
`$_FILES['INPUT_FIELD_NAME']['size']`

<br>

# Basic File Upload Script

<br>

## HTML Form Markup

````html
<form action="" method="post" enctype="multipart/form-data">
  <div class="mb-3">
  	<label for="image" class="mb-1">Select a File to Upload</label>
    <input type="hidden" name="MAX_FILE_SIZE" value="<?php echo $max; ?>" />
		<input type="file" class="form-control" name="image" id="image" />
  </div>
  <div class="mb-3">
    <input type="submit" class="submit-btn" name="upload" value="Upload" />
  </div>
</form>
````

## PHP Markup

> This PHP script will be placed on the same page as the form, above the DOCTYPE declaration
{.is-info}

<br>

````php
<?php
$max = 51200;

if (isset($_POST['upload'])){
	$destination = 'path/to/upload/tmp/dir';
  move_uploaded_file($_FILES['image']['tmp_name'], $destination . $_FILES['image']['name']);
}
````

## Showing the Filenames below the form

````php
</form>
<pre>
<?php
if (isset($_POST['upload'])){
	print_r($_FILES);
  }
?>
</pre>