[TOC]



# Grammar



## visibility(public, protected, private)

### public

---> available to access wherever u want

### protected

---> class itself and child class. That is passable.

### private

---> just class itself

## Boolean (special php)

---> if true, it puts one. if false, it puts zero



## Array (double)

want to put data, it will be like this

```
$a = ['one', 'two'], ['three', 'four']

echo ($a[0][0]) --> 'one'
```



## Str_replace

all words that matched the search word are mounted by the words

```php
str_replace ( array|string $search , array|string $replace , string|array $subject , int &$count = null ) : string|array
```

in case of that, all $search words are replaced to $replace.

#### === reference ===

#### PHP Official 

https://www.php.net/manual/ja/function.str-replace.php

## trim

Remove whitespace (in general) or other characters from the beginning and end of the string.

this is the easiest way to implement trim function.

```php
$value = trim($value)
```

#### === reference ===

#### PHP Official 

https://www.php.net/manual/en/function.trim.php

## Preg_replace

Perform a regular explanation search and replace

Ex) date

```php
<?php
$string = 'April 15, 2003';
$pattern = '/(\w+) (\d+), (\d+)/i';
$replacement = '${1}1,$3';
echo preg_replace($pattern, $replacement, $string);
?>
```

```
output == April1,2003
```



#### === 

#### php official

https://www.php.net/manual/en/function.preg-replace.php

# Words

## namespace



### ==== General description ====

Two people that have same name like hanako are not called by people 'Hanako' in case they are in the same space/room.

In above situation, most people tend to call them with family name or nickname or something..



### ==== php description ====

Official doc says

        Name collisions between code you create, and internal PHP classes/functions/constants or third-party classes/functions/constants.
        Ability to alias (or shorten) Extra_Long_Names designed to alleviate the first problem, improving readability of source code.
NOTICE 

write namespace top of the script absolutely

### ==== Error in namespace ====

namespace declation statement has to be the very first statement or after any declare call in the script.

This is the example of that error occurs

```
require 'some path';
namespace ~~~~
```



# From SQL

## orderby

it is useful to sort data by number or string value from mysql database.

In case of laravel, LARAVEL ORDERBY is also available.

===

#### PHP MySQL Use The ORDER BY Clause

https://www.w3schools.com/php/php_mysql_select_orderby.asp

===