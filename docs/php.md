# Quick overview of PHP

## Resources
This overview is mainly based on the following documents:
* https://www.php.net/docs.php

## What is PHP in a nutshell?

PHP is a scripting language, which can be directly embedded into HTML code, using the tags
``` php
<?php
  //Basic php code
  echo "Hello world!";
?>
```
In contrast to JavaScript the code is not evaluated on the client side, but instead on the server side.

## Basic syntax

### Data types
PHP has for basic types, known from many programming languages
``` php
<?php
  $a_string = "this is a string";
  $second_string = "This is also a string";
  $a_int = 5;
  $a_float = .4;
  $a_bool = TRUE; // bools are case insensitive, so True or true would work as well
?>
```
The type is not defined by the user but decided at runtime. To get the type of a variable, we can use `var_dump()`.

*Bools*

The following variables, if casted as a bool, are considered as false. Everything else is true
``` php
<? php
  $int = 0;
  $float_one = 0.0;
  $float_two = -0.0;
  $string_one = "";
  $string_two = "0";
  $empty_array = array();
  $null = NULL;
?>
```

*Integers*

* Integers can also be denoted in hexadecimal notation (with a preceding 0x), in octal notation (with a preceding 0o) or in binary notation (with a preceding 0b).
* For better readability integers can contain underscores between digits (only since PHP 7.4.0) e.g.
``` php
<? php
  $long_integer = 123_456_789;
?>
```
* If an integer overflows, it is casted into a float. Also there is no integer division. To achieve an integer division we can use `intdiv()`.
* Floats, which are casted to integers, are rounded towards 0.


*Floats*

* Floats can be defined using scientific notation, as well as underscores (similar to integers).
* some operations with floats can result in `NAN`. Any comparison of `NAN` with another value, except for `True`, will result in `False`, including a comparison with itself.


