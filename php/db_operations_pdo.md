---
title: Database Operations using PDO
description: 
published: true
date: 2022-10-10T18:02:17.928Z
tags: database, mysql, pdo, prepared-statements
editor: markdown
dateCreated: 2022-10-10T18:02:17.928Z
---

# Database Operations using PDO Breakdown

<br>

## PDO::prepare

<br>

> Prepares an SQL statement to be executed by the `PDOStatement::execute()` method. 

>The statement template can contain zero or more named (:name) or question mark (?) parameter markers for which real values will be substituted when the statement is executed. Both named and question mark parameter markers cannot be used within the same statement template; only one or the other parameter style. 

>Use these parameters to bind any user-input, do not include the user-input directly in the query. 

### Using Question Marks as Placeholder

````php

<?php
/* Execute a prepared statement by passing an array of values */
$sth = $dbh->prepare('SELECT name, colour, calories
    FROM fruit
    WHERE calories < ? AND colour = ?');
$sth->execute([150, 'red']);
$red = $sth->fetchAll();
$sth->execute([175, 'yellow']);
$yellow = $sth->fetchAll();
?>
````

### Using Named Parameters

````phpc

<?php
/* Execute a prepared statement by passing an array of values */
$sql = 'SELECT name, colour, calories
    FROM fruit
    WHERE calories < :calories AND colour = :colour';
$sth = $dbh->prepare($sql, [PDO::ATTR_CURSOR => PDO::CURSOR_FWDONLY]);
$sth->execute(['calories' => 150, 'colour' => 'red']);
$red = $sth->fetchAll();
/* Array keys can be prefixed with colons ":" too (optional) */
$sth->execute([':calories' => 175, ':colour' => 'yellow']);
$yellow = $sth->fetchAll();
?>

````

## PDOStatement::bindParam

> Binds a PHP variable to a corresponding named or question mark placeholder in the SQL statement that was used to prepare the statement. 

### Using Named Placeholders

````php
<?php
/* Execute a prepared statement by binding PHP variables */
$calories = 150;
$colour = 'red';
$sth = $dbh->prepare('SELECT name, colour, calories
    FROM fruit
    WHERE calories < :calories AND colour = :colour');
$sth->bindParam('calories', $calories, PDO::PARAM_INT);
/* Names can be prefixed with colons ":" too (optional) */
$sth->bindParam(':colour', $colour, PDO::PARAM_STR);
$sth->execute();
?>
````

### Using Question Mark Placeholders

````php
<?php
/* Execute a prepared statement by binding PHP variables */
$calories = 150;
$colour = 'red';
$sth = $dbh->prepare('SELECT name, colour, calories
    FROM fruit
    WHERE calories < ? AND colour = ?');
$sth->bindParam(1, $calories, PDO::PARAM_INT);
$sth->bindParam(2, $colour, PDO::PARAM_STR);
$sth->execute();
?>

````