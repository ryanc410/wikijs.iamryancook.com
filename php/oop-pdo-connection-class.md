---
title: PDO Connection Class
description: Example of using OOP to handle database actions in PHP
published: true
date: 2022-09-16T12:37:11.336Z
tags: php, database, oop, class, pdo
editor: markdown
dateCreated: 2022-09-14T11:55:02.312Z
---

# Database Class Example
````php
<?php
class DatabaseClass{	
	
        private $connection = null;

        // this function is called everytime this class is instantiated		
        public function __construct( $dbhost = "localhost", $dbname = "myDataBaseName", $username = "root", $password    = ""){

            try{
			
                $this->connection = new PDO("mysql:host={$dbhost};dbname={$dbname};", $username, $password);
                $this->connection->setAttribute(PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION);
                $this->connection->setAttribute(PDO::ATTR_DEFAULT_FETCH_MODE, PDO::FETCH_ASSOC);
				
            }catch(Exception $e){
                throw new Exception($e->getMessage());   
            }			
			
        }
		
        // Insert a row/s in a Database Table
        public function Insert( $statement = "" , $parameters = [] ){
            try{
				
                $this->executeStatement( $statement , $parameters );
                return $this->connection->lastInsertId();
				
            }catch(Exception $e){
                throw new Exception($e->getMessage());   
            }		
        }

        // Select a row/s in a Database Table
        public function Select( $statement = "" , $parameters = [] ){
            try{
				
                $stmt = $this->executeStatement( $statement , $parameters );
                return $stmt->fetchAll();
				
            }catch(Exception $e){
                throw new Exception($e->getMessage());   
            }		
        }
		
        // Update a row/s in a Database Table
        public function Update( $statement = "" , $parameters = [] ){
            try{
				
                $this->executeStatement( $statement , $parameters );
				
            }catch(Exception $e){
                throw new Exception($e->getMessage());   
            }		
        }		
		
        // Remove a row/s in a Database Table
        public function Remove( $statement = "" , $parameters = [] ){
            try{
				
                $this->executeStatement( $statement , $parameters );
				
            }catch(Exception $e){
                throw new Exception($e->getMessage());   
            }		
        }		
        
        // execute statement
        private function executeStatement( $statement = "" , $parameters = [] ){
            try{
			
                $stmt = $this->connection->prepare($statement);
                $stmt->execute($parameters);
                return $stmt;
				
            }catch(Exception $e){
                throw new Exception($e->getMessage());   
            }		
        }
		
    }
?>
````

# How to Use

## Create/Instantiate the Class
````php
    $db = new Database(
        "MySQLHost",
        "myDatabaseName",
        "myUserName",
        "myUserPassword"
    );

````

## Insert Example
````php
    $id = $db->Insert("Insert into `TableName`( `column1` , `column2`) values ( :column1 , :column2 )", [
        'column1' => 'column1 Value',
        'column2' => 'column2 Value',
    ]);
````

## Select Example
````php
 $db->Select("Select * from TableName");
````

## Update Example
````php
    $db->Update("Update TableName set `column1` = :column1 where id = :id",[
        'id' => 1,
        'column1' => 'a new column1 value'
    ]);
````

## Remove Example
````php
    $db->Remove("Delete from TableName where id = :id",[
        'id' => 1
    ]);
````