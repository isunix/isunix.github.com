---
layout: post
title: "Pro PHP and Jquery chap03: object oriented programming"
date: 2014-10-30 14:03:48 +0800
comments: true
categories: PHP
---
I have written some code in PHP, but I almost never use the object oriented way. Here below is some excerpts from the book "Pro PHP and Jquery".  

1.How to build a class and instantiate it.   

```php
<?php
  class MyClass{
    //class properties and methods go here
  }
  $obj = new MyClass;
  var_dump($obj);
?>
```  

It gives out something like 

```php
object(MyClass)#1 (0) { }
```

2.The following code shows how to set and read out a class property.  

```php
<?php
  class MyClass{
    //class properties and methods go here
    public $prop1 = "I'm a class property!";
  }

  $obj = new MyClass;
  echo $obj->prop1;
?>
```   

3.THe following code shows how to define methods in php. Methods are class-specific functions:  

```php
<?php
class MyClass {
  public $prop1 = "I'm a class property!";
  public function setProperty($newval){
    $this->prop1 = $newval;
  }

  public function getProperty(){
    return $this->prop1 . "<br />";
  }
}

$obj = new MyClass;
echo $obj->prop1;

?>
```

4.Use of contructor methods:

```php
<?php
class MyClass
{
  public $prop1 = "I'm a class property!";

  public function __construct()
  {
    echo 'The class "', __CLASS__, '" was initiated!<br />';
  }

  public function setProperty($newval)
  {
    $this->prop1 = $newval;
  }

  public function getProperty()
  {
    return $this->prop1 . "<br />";
  }
}

// Create a new object
$obj = new MyClass;
// Get the value of $prop1
echo $obj->getProperty();
// Output a message at the end of the file
echo "End of file.<br />";
?>
```
		


