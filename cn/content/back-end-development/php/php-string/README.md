#PHP 5 Strings

A string is a sequence of characters, like "Hello world!".

PHP String Functions
In this chapter we will look at some commonly used functions to manipulate strings.

Get The Length of a String
The PHP strlen() function returns the length of a string.

The example below returns the length of the string "Hello world!":

Example
```php
<?php
echo strlen("Hello world!"); // outputs 12
?>
```
The output of the code above will be: 12.

Count The Number of Words in a String
The PHP str_word_count() function counts the number of words in a string:

Example
```php
<?php
echo str_word_count("Hello world!"); // outputs 2
?>
```
The output of the code above will be: 2.

Reverse a String
The PHP strrev() function reverses a string:

Example
```php
<?php
echo strrev("Hello world!"); // outputs !dlrow olleH
?>
```
The output of the code above will be: !dlrow olleH.

Search For a Specific Text Within a String
The PHP strpos() function searches for a specific text within a string.

If a match is found, the function returns the character position of the first match. If no match is found, it will return FALSE.

The example below searches for the text "world" in the string "Hello world!":

Example
```php
<?php
echo strpos("Hello world!", "world"); // outputs 6
?>
```
The output of the code above will be: 6.

Tip: The first character position in a string is 0 (not 1).

Replace Text Within a String
The PHP str_replace() function replaces some characters with some other characters in a string.

The example below replaces the text "world" with "Dolly":

Example
```php
<?php
echo str_replace("world", "Dolly", "Hello world!"); // outputs Hello Dolly!
?>
```
The output of the code above will be: Hello Dolly!

Complete PHP String Reference
For a complete reference of all string functions, go to our complete PHP String Reference.

The PHP string reference contains description and example of use, for each function!