# PHP Basics 🚀

Welcome to this learning guide on PHP! This document covers the **fundamental concepts** I needed to get started with PHP.

---

## 📌 1. Introduction to PHP
**PHP (Hypertext Preprocessor)** is a popular server-side scripting language used for web development.  
✅ It is **open-source** and widely used for building **dynamic web applications**.  
✅ PHP code is **executed on the server**, and the result is sent to the browser.  

### **Hello World Example**
```php
<?php
echo "Hello, World!";
?>
```
## Basic Syntax
### Variables in PHP
- Variables start with ``` $ ``` and are case-sensitive.
- PHP is dynamically typed (no need to declare type explicitly).

Example: 
```php
$name = "John";  // String
$age = 25;       // Integer
$price = 99.99;  // Float
$isAdmin = true; // Boolean

```
### Data Types in PHP
- **String:** ``` "Hello, PHP!" ```
- **Integer:** ``` 42```
- **Float:** ``` 3.14 ```
- **Boolean:** ``` true/false ```
- **Array:** ``` $fruits = ["apple" , "banana", "orange"]; ```
- **NULL:** Represent no value
- To know about data type we can use ``` gettype() ``` or ``` var_dump() ```.
- PHP automatically determine the datatype during the runtime.

### Operators
Operators perform operations on variables and values: 
- **Arithmetic:** ``` + - * / % (modulus) ```

- **Comparison:** ``` == != < > <= >=  ```

- **Logical:** ```&& (AND) || (OR) ! (NOT) ```

- **Assignment Operators:** ```= += -= *= /= ```

- **String Operators:** ``` . += ``` 

- **Error Control Operators:** ``` @ ``` 

- **Increment Operator:** ``` ++ ```

- **Decrement Operator:** ``` -- ``` 

- **Bitwise Operator:** ```& | ^ ~ << >>  ```

- **Array Operators** 

- ** Execution Operators:** ``` `` ``` 

- **Type Operators:** ``` instanceof ``` 

- **Nullsafe Operator:** ``` ? ``` 

## Conditional Statements

Used to execute code based on conditions:

- **if:** Executes if a condition is true.
- **else:** Executes if the ```if``` condition is false.
- **else if:** Checks additional conditions.
Examples:
``if-else`` Statement
```php
$age = 20;
if ($age >= 18) {
    echo "You are an adult.";
} else {
    echo "You are a minor.";
}
```

``` switch ``` Statement
```php
$day = "Monday";
switch ($day) {
    case "Monday":
        echo "Start of the week!";
        break;
    case "Friday":
        echo "Weekend is near!";
        break;
    default:
        echo "A regular day!";
}

```

## Loop in PHP
Loops in PHP allow repetitive execution of a code block, which is essential for tasks like processing lists, generating sequences, or iterating over data. PHP supports four main loop types: for, while, do-while, and foreach. Below, I’ll detail each with examples and practical insights gained during this sprint. 

### 1. ```for``` loop
The for loop is ideal when you know the exact number of iterations beforehand. It consists of three parts: initialization, condition, and increment/decrement. 

U**se Case:** Generating a fixed number of HTML elements (e.g., table rows) or iterating over a known range. 

Examples:
```php
for ($i = 1; $i <= 5; $i++) {
    echo "Iteration: $i\n";
}
```

### 2. ```while``` loop
The while loop executes as long as a condition remains true. It’s useful when the number of iterations isn’t predetermined. 
Examples:
```php
$count = 3;
while ($count > 0) {
    echo "Countdown: $count\n";
    $count--;
}

```

### 3. ``` do-while ``` loop
The do-while loop is similar to while, but it guarantees the code block runs at least once before checking the condition. 

**Use Case:** Scenarios where an action must occur at least once, like prompting a user for input before validation. 

Example:
```php
$x = 1;
do {
    echo "Value: $x\n";
    $x++;
} while ($x <= 5);

```

### 4.```for-each``` loop
The foreach loop is designed specifically for iterating over arrays or objects. It simplifies working with collections. 
Example:
```php
$fruits = ["Apple", "Banana", "Mango"];
foreach ($fruits as $fruit) {
    echo "Fruit: $fruit\n";
}
```
### Loop Control ```break``` and ```continue```
PHP provides two keywords to control loop execution: 

- **break:** Exits the loop entirely. 

- **continue:** Skips the current iteration and moves to the next. 

**Use Case:** Filtering data (e.g., skipping invalid entries) or stopping a loop when a condition is met (e.g., finding a match). 
Example:
```php
for ($i = 1; $i <= 5; $i++) {
    if ($i == 3) break;  // Stops loop when i = 3
    echo "Number: $i\n";
}
```

```php
for ($i = 1; $i <= 5; $i++) {
    if ($i == 3) continue;  // ignore iteration when i = 3
    echo "Number: $i\n";
}
```

## Basic Input and Output Handling
Handling user input and displaying output is crucial in PHP.
- ```echo``` vs ```print```
```php
echo "Hello, World!";  // No return value
print "Hello, PHP!";   // Returns 1
```
**Reading Input from Console**
```php
echo "Enter your name: ";
$name = trim(fgets(STDIN));
echo "Hello, $name!";
```

## Function in PHP

#### 1. **Function Definition**
A function in PHP is defined using the `function` keyword followed by the function name and parentheses `()`.

```php
function functionName() {
    // code to be executed
}
```

#### 2. **Function Naming**
- Function names should be descriptive and follow naming conventions.
- Use camelCase for naming functions (e.g., `calculateSum`).

#### 3. **Parameters**
Functions can accept parameters, which are variables passed to the function. Parameters are defined within the parentheses.

```php
function greet($name) {
    return "Hello, " . $name . "!";
}
```

#### 4. **Default Parameters**
You can set default values for parameters. If no argument is provided, the default value is used.

```php
function greet($name = "Guest") {
    return "Hello, " . $name . "!";
}
```

#### 5. **Return Values**
Functions can return values using the `return` keyword. This allows the function to send back a result.

```php
function add($a, $b) {
    return $a + $b;
}
```

#### 6. **Variable Scope**
Variables defined inside a function are local to that function and cannot be accessed outside of it. Use `global` keyword to access global variables.

```php
$globalVar = "I am global";

function testScope() {
    global $globalVar;
    echo $globalVar;
}
```

#### 7. **Calling Functions**
To execute a function, you call it by its name followed by parentheses. If the function requires parameters, you pass them within the parentheses.

```php
echo greet("Alice"); // Outputs: Hello, Alice!
```

#### 8. **Anonymous Functions**
PHP supports anonymous functions (closures), which can be assigned to variables and passed as arguments.

```php
$greet = function($name) {
    return "Hello, " . $name . "!";
};

echo $greet("Bob"); // Outputs: Hello, Bob!
```

#### 9. **Recursive Functions**
A function can call itself. This is useful for tasks that can be broken down into smaller, repetitive tasks.

```php
function factorial($n) {
    if ($n <= 1) {
        return 1;
    } else {
        return $n * factorial($n - 1);
    }
}

echo factorial(5); // Outputs: 120
```

### Example: Comprehensive Function

Here's a more complex example that includes multiple parameters, default values, and return statements:

```php
<?php
function calculateArea($length, $width = 10) {
    $area = $length * $width;
    return $area;
}

echo calculateArea(5); // Outputs: 50
echo calculateArea(5, 20); // Outputs: 100
?>
```

Sure! Here's a detailed guide on how to write nested functions in PHP:

### Nested Functions in PHP

#### 1. **Definition of Nested Functions**
Nested functions are functions defined within other functions. This allows for encapsulation and can be useful for organizing code logically.

#### 2. **Scope and Accessibility**
Nested functions are only accessible within the scope of the outer function. They cannot be called directly from outside the outer function.

### Example

```php
<?php
function outerFunction($outerParam) {
    // Define a nested function
    function innerFunction($innerParam) {
        return "Inner Function: " . $innerParam;
    }

    // Call the nested function within the outer function
    $innerResult = innerFunction($outerParam);
    return "Outer Function: " . $outerParam . " | " . $innerResult;
}

// Call the outer function
echo outerFunction("Test");
?>
```

### Practical Use Case

Nested functions can be useful in scenarios where you need to perform a series of related tasks. For example, validating and processing user input:

```php
<?php
function processInput($input) {
    // Nested function to validate input
    function validate($data) {
        if (empty($data)) {
            return "Invalid input";
        }
        return "Valid input";
    }

    // Nested function to sanitize input
    function sanitize($data) {
        return htmlspecialchars($data);
    }

    // Validate and sanitize input
    $validationResult = validate($input);
    if ($validationResult === "Valid input") {
        $sanitizedInput = sanitize($input);
        return "Processed Input: " . $sanitizedInput;
    } else {
        return $validationResult;
    }
}

// Call the outer function
echo processInput("<script>alert('Hello');</script>");
?>
```


### Example: Strict Types in PHP
We can declare the return type of function too.

```php
<?php
declare(strict_types=1);

function multiply(int $a, int $b): int {
    return $a * $b;
}

echo multiply(3, 4); // Outputs: 12
?>
```

## Pass by Value vs Pass by reference

### Pass by Value

When you pass arguments by value, PHP copies the value of the argument into the function. Changes made to the argument inside the function do not affect the original value.

### Example: Pass by Value

```php
<?php
function addTen($number) {
    $number += 10;
    return $number;
}

$originalNumber = 5;
echo addTen($originalNumber); // Outputs: 15
echo $originalNumber; // Outputs: 5 (unchanged)
?>
```

### Pass by Reference

When you pass arguments by reference, PHP passes a reference to the variable. Changes made to the argument inside the function affect the original value.

### Example: Pass by Reference

```php
<?php
function addTen(&$number) {
    $number += 10;
}

$originalNumber = 5;
addTen($originalNumber);
echo $originalNumber; // Outputs: 15 (changed)
?>
```

## Variadic Function

A variadic function in PHP is a function that can accept a variable number of arguments. This is useful when you don't know in advance how many arguments will be passed to the function.

### Defining a Variadic Function

In PHP, you can define a variadic function using the `...` (splat) operator before the parameter name. This parameter will then be an array containing all the arguments passed to the function.

### Example

```php
<?php
function sum(...$numbers) {
    $total = 0;
    foreach ($numbers as $number) {
        $total += $number;
    }
    return $total;
}

echo sum(1, 2, 3, 4); // Outputs: 10
echo sum(5, 10); // Outputs: 15
?>
```

## String Manipulation in PHP

PHP offers a wide range of functions for string manipulation. Here's a comprehensive list of these functions along with brief descriptions and examples:

### Basic String Functions

1. **Concatenation**: Use the `.` operator to concatenate strings.
   ```php
   $str1 = "Hello";
   $str2 = "World";
   $result = $str1 . " " . $str2; // Outputs: Hello World
   ```

2. **String Length**: Use `strlen()` to get the length of a string.
   ```php
   $str = "Hello, World!";
   echo strlen($str); // Outputs: 13
   ```

3. **Substring**: Use `substr()` to extract a part of a string.
   ```php
   $str = "Hello, World!";
   echo substr($str, 7, 5); // Outputs: World
   ```

### Case Conversion

4. **To Upper Case**: Use `strtoupper()` to convert a string to upper case.
   ```php
   $str = "hello";
   echo strtoupper($str); // Outputs: HELLO
   ```

5. **To Lower Case**: Use `strtolower()` to convert a string to lower case.
   ```php
   $str = "HELLO";
   echo strtolower($str); // Outputs: hello
   ```

6. **First Character to Upper Case**: Use `ucfirst()` to capitalize the first character.
   ```php
   $str = "hello";
   echo ucfirst($str); // Outputs: Hello
   ```

7. **First Character of Each Word to Upper Case**: Use `ucwords()` to capitalize the first character of each word.
   ```php
   $str = "hello world";
   echo ucwords($str); // Outputs: Hello World
   ```

### Trimming

8. **Trim**: Use `trim()` to remove whitespace from both ends of a string.
   ```php
   $str = "  hello  ";
   echo trim($str); // Outputs: hello
   ```

9. **Left Trim**: Use `ltrim()` to remove whitespace from the beginning of a string.
   ```php
   $str = "  hello";
   echo ltrim($str); // Outputs: hello
   ```

10. **Right Trim**: Use `rtrim()` to remove whitespace from the end of a string.
   ```php
   $str = "hello  ";
   echo rtrim($str); // Outputs: hello
   ```

### Searching and Replacing

11. **String Position**: Use `strpos()` to find the position of the first occurrence of a substring.
    ```php
    $str = "Hello, World!";
    echo strpos($str, "World"); // Outputs: 7
    ```

12. **String Replace**: Use `str_replace()` to replace all occurrences of a search string with a replacement string.
    ```php
    $str = "Hello, World!";
    echo str_replace("World", "PHP", $str); // Outputs: Hello, PHP!
    ```

13. **Case-Insensitive Replace**: Use `str_ireplace()` for case-insensitive replacement.
    ```php
    $str = "Hello, World!";
    echo str_ireplace("world", "PHP", $str); // Outputs: Hello, PHP!
    ```

### Splitting and Joining

14. **Explode**: Use `explode()` to split a string into an array.
    ```php
    $str = "apple,banana,cherry";
    $array = explode(",", $str);
    print_r($array); // Outputs: Array ( [0] => apple [1] => banana [2] => cherry )
    ```

15. **Implode**: Use `implode()` to join array elements into a string.
    ```php
    $array = ["apple", "banana", "cherry"];
    echo implode(", ", $array); // Outputs: apple, banana, cherry
    ```

### Formatting

16. **String Formatting**: Use `sprintf()` to format a string.
    ```php
    $num = 5;
    $location = "tree";
    echo sprintf("There are %d monkeys in the %s", $num, $location); // Outputs: There are 5 monkeys in the tree
    ```

### Comparison

17. **String Comparison**: Use `strcmp()` to compare two strings.
    ```php
    $str1 = "Hello";
    $str2 = "hello";
    echo strcmp($str1, $str2); // Outputs: -1 (because "Hello" is less than "hello" in ASCII)
    ```

18. **Case-Insensitive Comparison**: Use `strcasecmp()` for case-insensitive comparison.
    ```php
    $str1 = "Hello";
    $str2 = "hello";
    echo strcasecmp($str1, $str2); // Outputs: 0 (because "Hello" is equal to "hello" ignoring case)
    ```

### Encoding and Decoding

19. **HTML Entities**: Use `htmlentities()` to convert characters to HTML entities.
    ```php
    $str = "<a href='test'>Test</a>";
    echo htmlentities($str); // Outputs: &lt;a href='test'&gt;Test&lt;/a&gt;
    ```

20. **HTML Special Characters**: Use `htmlspecialchars()` to convert special characters to HTML entities.
    ```php
    $str = "<a href='test'>Test</a>";
    echo htmlspecialchars($str); // Outputs: &lt;a href='test'&gt;Test&lt;/a&gt;
    ```

### Miscellaneous

21. **Repeat**: Use `str_repeat()` to repeat a string.
    ```php
    $str = "Hello";
    echo str_repeat($str, 3); // Outputs: HelloHelloHello
    ```

22. **Reverse**: Use `strrev()` to reverse a string.
    ```php
    $str = "Hello";
    echo strrev($str); // Outputs: olleH
    ```

23. **Word Count**: Use `str_word_count()` to count the number of words in a string.
    ```php
    $str = "Hello, World!";
    echo str_word_count($str); // Outputs: 2
    ```

## Array and Array Functions


### Array Basics

#### 1. **Creating Arrays**

- **Indexed Arrays**: Arrays with numeric indexes.
  ```php
  $indexedArray = ["apple", "banana", "cherry"];
  ```

- **Associative Arrays**: Arrays with named keys.
  ```php
  $associativeArray = ["name" => "John", "age" => 30, "city" => "New York"];
  ```

- **Multidimensional Arrays**: Arrays containing one or more arrays.
  ```php
  $multiArray = [
      ["name" => "John", "age" => 30],
      ["name" => Jane", "age" => 25]
  ];
  ```

### Array Functions

#### 2. **Adding Elements**

- **array_push()**: Adds one or more elements to the end of an array.
  ```php
  $array = ["apple", "banana"];
  array_push($array, "cherry", "date");
  print_r($array); // Outputs: Array ( [0] => apple [1] => banana [2] => cherry [3] => date )
  ```

- **array_unshift()**: Adds one or more elements to the beginning of an array.
  ```php
  $array = ["banana", "cherry"];
  array_unshift($array, "apple");
  print_r($array); // Outputs: Array ( [0] => apple [1] => banana [2] => cherry )
  ```

#### 3. **Removing Elements**

- **array_pop()**: Removes the last element of an array.
  ```php
  $array = ["apple", "banana", "cherry"];
  array_pop($array);
  print_r($array); // Outputs: Array ( [0] => apple [1] => banana )
  ```

- **array_shift()**: Removes the first element of an array.
  ```php
  $array = ["apple", "banana", "cherry"];
  array_shift($array);
  print_r($array); // Outputs: Array ( [0] => banana [1] => cherry )
  ```

#### 4. **Array Length**

- **count()**: Returns the number of elements in an array.
  ```php
  $array = ["apple", "banana", "cherry"];
  echo count($array); // Outputs: 3
  ```

#### 5. **Array Search**

- **in_array()**: Checks if a value exists in an array.
  ```php
  $array = ["apple", "banana", "cherry"];
  echo in_array("banana", $array); // Outputs: 1 (true)
  ```

- **array_search()**: Searches for a value and returns the corresponding key.
  ```php
  $array = ["apple", "banana", "cherry"];
  echo array_search("banana", $array); // Outputs: 1
  ```

#### 6. **Array Sorting**

- **sort()**: Sorts an array in ascending order.
  ```php
  $array = ["cherry", "banana", "apple"];
  sort($array);
  print_r($array); // Outputs: Array ( [0] => apple [1] => banana [2] => cherry )
  ```

- **rsort()**: Sorts an array in descending order.
  ```php
  $array = ["cherry", "banana", "apple"];
  rsort($array);
  print_r($array); // Outputs: Array ( [0] => cherry [1] => banana [2] => apple )
  ```

- **asort()**: Sorts an associative array in ascending order, according to the value.
  ```php
  $array = ["a" => "cherry", "b" => "banana", "c" => "apple"];
  asort($array);
  print_r($array); // Outputs: Array ( [c] => apple [b] => banana [a] => cherry )
  ```

- **ksort()**: Sorts an associative array in ascending order, according to the key.
  ```php
  $array = ["c" => "apple", "b" => "banana", "a" => "cherry"];
  ksort($array);
  print_r($array); // Outputs: Array ( [a] => cherry [b] => banana [c] => apple )
  ```

#### 7. **Array Filtering**

- **array_filter()**: Filters elements of an array using a callback function.
  ```php
  $array = [1, 2, 3, 4, 5];
  $even = array_filter($array, function($value) {
      return $value % 2 === 0;
  });
  print_r($even); // Outputs: Array ( [1] => 2 [3] => 4 )
  ```

#### 8. **Array Mapping**

- **array_map()**: Applies a callback function to the elements of an array.
  ```php
  $array = [1, 2, 3, 4, 5];
  $squared = array_map(function($value) {
      return $value * $value;
  }, $array);
  print_r($squared); // Outputs: Array ( [0] => 1 [1] => 4 [2] => 9 [3] => 16 [4] => 25 )
  ```

#### 9. **Array Reduction**

- **array_reduce()**: Reduces an array to a single value using a callback function.
  ```php
  $array = [1, 2, 3, 4, 5];
  $sum = array_reduce($array, function($carry, $item) {
      return $carry + $item;
  }, 0);
  echo $sum; // Outputs: 15
  ```

#### 10. **Array Merging**

- **array_merge()**: Merges one or more arrays.
  ```php
  $array1 = ["apple", "banana"];
  $array2 = ["cherry", "date"];
  $merged = array_merge($array1, $array2);
  print_r($merged); // Outputs: Array ( [0] => apple [1] => banana [2] => cherry [3] => date )
  ```

#### 11. **Array Slicing**

- **array_slice()**: Extracts a slice of an array.
  ```php
  $array = ["apple", "banana", "cherry", "date"];
  $slice = array_slice($array, 1, 2);
  print_r($slice); // Outputs: Array ( [0] => banana [1] => cherry )
  ```

#### 12. **Array Splicing**

- **array_splice()**: Removes a portion of the array and replaces it with something else.
  ```php
  $array = ["apple", "banana", "cherry", "date"];
  array_splice($array, 1, 2, ["kiwi", "lemon"]);
  print_r($array); // Outputs: Array ( [0] => apple [1] => kiwi [2] => lemon [3] => date )
  ```

#### 13. **Array Keys and Values**

- **array_keys()**: Returns all the keys of an array.
  ```php
  $array = ["name" => "John", "age" => 30, "city" => "New York"];
  $keys = array_keys($array);
  print_r($keys); // Outputs: Array ( [0] => name [1] => age [2] => city )
  ```

- **array_values()**: Returns all the values of an array.
  ```php
  $array = ["name" => "John", "age" => 30, "city" => "New York"];
  $values = array_values($array);
  print_r($values); // Outputs: Array ( [0] => John [1] => 30 [2] => New York )
  ```

#### 14. **Array Unique**

- **array_unique()**: Removes duplicate values from an array.
  ```php
  $array = ["apple", "banana", "apple", "cherry"];
  $unique = array_unique($array);
  print_r($unique); // Outputs: Array ( [0] => apple [1] => banana [3] => cherry )
  ```

#### 15. **Array Intersect**

- **array_intersect()**: Computes the intersection of arrays.
  ```php
  $array1 = ["apple", "banana", "cherry"];
  $array2 = ["banana", "cherry", "date"];
  $intersection = array_intersect($array1, $array2);
  print_r($intersection); // Outputs: Array ( [1] => banana [2] => cherry )
  ```

#### 16. **Array Difference**

- **array_diff()**: Computes the difference of arrays.
  ```php
  $array1 = ["apple", "banana", "cherry"];
  $array2 = ["banana", "cherry", "date"];
  $difference = array_diff($array1, $array2);
  print_r($difference); // Outputs: Array ( [0] => apple )
  ```


#### 17. **Array Combine**

- **array_combine()**: Creates an array by using one array for keys and another for values.
  ```php
  $keys = ["name", "age", "city"];
  $values = ["John", 30, "New York"];
  $combined = array_combine($keys, $values);
  print_r($combined); // Outputs: Array ( [name] => John [age] => 30 [city] => New York )
  ```

#### 18. **Array Flip**

- **array_flip()**: Exchanges all keys with their associated values in an array.
  ```php
  $array = ["a" => "apple", "b" => "banana", "c" => "cherry"];
  $flipped = array_flip($array);
  print_r($flipped); // Outputs: Array ( [apple] => a [banana] => b [cherry] => c )
  ```

#### 19. **Array Reverse**

- **array_reverse()**: Returns an array with elements in reverse order.
  ```php
  $array = ["apple", "banana", "cherry"];
  $reversed = array_reverse($array);
  print_r($reversed); // Outputs: Array ( [0] => cherry [1] => banana [2] => apple )
  ```

#### 20. **Array Chunk**

- **array_chunk()**: Splits an array into chunks.
  ```php
  $array = ["apple", "banana", "cherry", "date"];
  $chunks = array_chunk($array, 2);
  print_r($chunks); // Outputs: Array ( [0] => Array ( [0] => apple [1] => banana ) [1] => Array ( [0] => cherry [1] => date ) )
  ```

#### 21. **Array Key Exists**

- **array_key_exists()**: Checks if the specified key exists in the array.
  ```php
  $array = ["name" => "John", "age" => 30];
  echo array_key_exists("name", $array); // Outputs: 1 (true)
  ```

#### 22. **Array Fill**

- **array_fill()**: Fills an array with values.
  ```php
  $filled = array_fill(0, 5, "apple");
  print_r($filled); // Outputs: Array ( [0] => apple [1] => apple [2] => apple [3] => apple [4] => apple )
  ```

#### 23. **Array Fill Keys**

- **array_fill_keys()**: Fills an array with values, specifying keys.
  ```php
  $keys = ["a", "b", "c"];
  $filled = array_fill_keys($keys, "apple");
  print_r($filled); // Outputs: Array ( [a] => apple [b] => apple [c] => apple )
  ```

#### 24. **Array Walk**

- **array_walk()**: Applies a user function to every member of an array.
  ```php
  $array = ["apple", "banana", "cherry"];
  array_walk($array, function(&$value, $key) {
      $value = strtoupper($value);
  });
  print_r($array); // Outputs: Array ( [0] => APPLE [1] => BANANA [2] => CHERRY )
  ```

#### 25. **Array Walk Recursive**

- **array_walk_recursive()**: Applies a user function recursively to every member of an array.
  ```php
  $array = ["fruits" => ["apple", "banana"], "vegetables" => ["carrot", "pea"]];
  array_walk_recursive($array, function(&$value, $key) {
      $value = strtoupper($value);
  });
  print_r($array); // Outputs: Array ( [fruits] => Array ( [0] => APPLE [1] => BANANA ) [vegetables] => Array ( [0] => CARROT [1] => PEA ) )
  ```

#### 26. **Array Diff Key**

- **array_diff_key()**: Computes the difference of arrays using keys for comparison.
  ```php
  $array1 = ["a" => "apple", "b" => "banana", "c" => "cherry"];
  $array2 = ["a" => "apple", "b" => "banana"];
  $diff = array_diff_key($array1, $array2);
  print_r($diff); // Outputs: Array ( [c] => cherry )
  ```

#### 27. **Array Intersect Key**

- **array_intersect_key()**: Computes the intersection of arrays using keys for comparison.
  ```php
  $array1 = ["a" => "apple", "b" => "banana", "c" => "cherry"];
  $array2 = ["a" => "apple", "b" => "banana"];
  $intersection = array_intersect_key($array1, $array2);
  print_r($intersection); // Outputs: Array ( [a] => apple [b] => banana )
  ```

#### 28. **Array Pad**

- **array_pad()**: Pads an array to the specified length with a value.
  ```php
  $array = ["apple", "banana"];
  $padded = array_pad($array, 5, "cherry");
  print_r($padded); // Outputs: Array ( [0] => apple [1] => banana [2] => cherry [3] => cherry [4] => cherry )
  ```

#### 29. **Array Product**

- **array_product()**: Calculates the product of values in an array.
  ```php
  $array = [1, 2, 3, 4];
  echo array_product($array); // Outputs: 24
  ```

#### 30. **Array Sum**

- **array_sum()**: Calculates the sum of values in an array.
  ```php
  $array = [1, 2, 3, 4];
  echo array_sum($array); // Outputs: 10
  ```
## Date Operations in PHP
PHP provides a robust set of functions for handling date and time operations. Here's a comprehensive guide covering everything you need to know about date operations in PHP:

### Basic Date and Time Functions

#### 1. **Getting the Current Date and Time**

- **date()**: Formats a local date and time.
  ```php
  echo date("Y-m-d H:i:s"); // Outputs: 2025-03-27 16:08:29 (example)
  ```

- **time()**: Returns the current Unix timestamp.
  ```php
  echo time(); // Outputs: 1616839709 (example)
  ```

#### 2. **Creating Date and Time**

- **mktime()**: Returns the Unix timestamp for a date.
  ```php
  $timestamp = mktime(0, 0, 0, 3, 27, 2025);
  echo date("Y-m-d H:i:s", $timestamp); // Outputs: 2025-03-27 00:00:00
  ```

- **strtotime()**: Parses an English textual datetime into a Unix timestamp.
  ```php
  $timestamp = strtotime("next Monday");
  echo date("Y-m-d H:i:s", $timestamp); // Outputs: 2025-03-31 00:00:00 (example)
  ```

### Formatting Dates and Times

#### 3. **Date Formatting**

- **date()**: Formats a local date and time.
  ```php
  echo date("l, F j, Y"); // Outputs: Thursday, March 27, 2025 (example)
  ```

- **DateTime::format()**: Formats a date and time using the DateTime object.
  ```php
  $date = new DateTime();
  echo $date->format("Y-m-d H:i:s"); // Outputs: 2025-03-27 16:08:29 (example)
  ```

### Working with DateTime Objects

#### 4. **Creating DateTime Objects**

- **new DateTime()**: Creates a new DateTime object.
  ```php
  $date = new DateTime();
  echo $date->format("Y-m-d H:i:s"); // Outputs: 2025-03-27 16:08:29 (example)
  ```

- **DateTime::createFromFormat()**: Creates a DateTime object from a specific format.
  ```php
  $date = DateTime::createFromFormat("Y-m-d", "2025-03-27");
  echo $date->format("Y-m-d H:i:s"); // Outputs: 2025-03-27 00:00:00
  ```

#### 5. **Modifying DateTime Objects**

- **DateTime::modify()**: Modifies the timestamp of a DateTime object.
  ```php
  $date = new DateTime();
  $date->modify("+1 day");
  echo $date->format("Y-m-d H:i:s"); // Outputs: 2025-03-28 16:08:29 (example)
  ```

- **DateTime::add()**: Adds an interval to a DateTime object.
  ```php
  $date = new DateTime();
  $interval = new DateInterval("P1D");
  $date->add($interval);
  echo $date->format("Y-m-d H:i:s"); // Outputs: 2025-03-28 16:08:29 (example)
  ```

- **DateTime::sub()**: Subtracts an interval from a DateTime object.
  ```php
  $date = new DateTime();
  $interval = new DateInterval("P1D");
  $date->sub($interval);
  echo $date->format("Y-m-d H:i:s"); // Outputs: 2025-03-26 16:08:29 (example)
  ```

### Date and Time Intervals

#### 6. **Creating Intervals**

- **DateInterval**: Represents a date interval.
  ```php
  $interval = new DateInterval("P2W");
  ```

- **DateInterval::createFromDateString()**: Creates a DateInterval from a relative time string.
  ```php
  $interval = DateInterval::createFromDateString("2 weeks");
  ```

#### 7. **Using Intervals with DateTime**

- **DateTime::add()**: Adds an interval to a DateTime object.
  ```php
  $date = new DateTime();
  $interval = new DateInterval("P2W");
  $date->add($interval);
  echo $date->format("Y-m-d H:i:s"); // Outputs: 2025-04-10 16:08:29 (example)
  ```

- **DateTime::sub()**: Subtracts an interval from a DateTime object.
  ```php
  $date = new DateTime();
  $interval = new DateInterval("P2W");
  $date->sub($interval);
  echo $date->format("Y-m-d H:i:s"); // Outputs: 2025-03-13 16:08:29 (example)
  ```

### Comparing Dates

#### 8. **DateTime::diff()**

- **DateTime::diff()**: Returns the difference between two DateTime objects.
  ```php
  $date1 = new DateTime("2025-03-27");
  $date2 = new DateTime("2025-04-10");
  $diff = $date1->diff($date2);
  echo $diff->format("%R%a days"); // Outputs: +14 days
  ```

### Timezones

#### 9. **Setting Timezones**

- **DateTimeZone**: Represents a timezone.
  ```php
  $timezone = new DateTimeZone("America/New_York");
  ```

- **DateTime::setTimezone()**: Sets the timezone for a DateTime object.
  ```php
  $date = new DateTime("now", new DateTimeZone("UTC"));
  $date->setTimezone(new DateTimeZone("America/New_York"));
  echo $date->format("Y-m-d H:i:s"); // Outputs: 2025-03-27 12:08:29 (example)
  ```

### Miscellaneous

#### 10. **Checkdate()**

- **checkdate()**: Validates a Gregorian date.
  ```php
  if (checkdate(2, 29, 2024)) {
      echo "Valid date";
  } else {
      echo "Invalid date";
  }
  // Outputs: Valid date (2024 is a leap year)
  ```

## File Handling in PHP
File handling is an essential part of PHP programming, allowing you to read, write, and manipulate files on the server.

### Basic File Operations

#### 1. **Opening and Closing Files**

- **fopen()**: Opens a file or URL.
  ```php
  $file = fopen("example.txt", "r"); // Opens the file for reading
  ```

- **fclose()**: Closes an open file.
  ```php
  fclose($file);
  ```

#### 2. **Reading Files**

- **fread()**: Reads from an open file.
  ```php
  $file = fopen("example.txt", "r");
  $content = fread($file, filesize("example.txt"));
  fclose($file);
  echo $content;
  ```

- **fgets()**: Reads a line from an open file.
  ```php
  $file = fopen("example.txt", "r");
  while ($line = fgets($file)) {
      echo $line;
  }
  fclose($file);
  ```

- **file_get_contents()**: Reads the entire file into a string.
  ```php
  $content = file_get_contents("example.txt");
  echo $content;
  ```

#### 3. **Writing Files**

- **fwrite()**: Writes to an open file.
  ```php
  $file = fopen("example.txt", "w");
  fwrite($file, "Hello, World!");
  fclose($file);
  ```

- **file_put_contents()**: Writes a string to a file.
  ```php
  file_put_contents("example.txt", "Hello, World!");
  ```

### File Modes

#### 4. **File Modes for fopen()**

- **"r"**: Read-only. Starts at the beginning of the file.
- **"r+"**: Read/Write. Starts at the beginning of the file.
- **"w"**: Write-only. Opens and truncates the file; or creates a new file if it doesn't exist.
- **"w+"**: Read/Write. Opens and truncates the file; or creates a new file if it doesn't exist.
- **"a"**: Write-only. Opens and writes to the end of the file or creates a new file if it doesn't exist.
- **"a+"**: Read/Write. Preserves file content by writing to the end of the file.
- **"x"**: Write-only. Creates a new file. Returns FALSE if the file already exists.
- **"x+"**: Read/Write. Creates a new file. Returns FALSE if the file already exists.

### File Information

#### 5. **Getting File Information**

- **filesize()**: Gets the size of a file.
  ```php
  echo filesize("example.txt"); // Outputs: 123 (example size in bytes)
  ```

- **file_exists()**: Checks if a file or directory exists.
  ```php
  if (file_exists("example.txt")) {
      echo "File exists";
  } else {
      echo "File does not exist";
  }
  ```

- **is_readable()**: Tells whether a file exists and is readable.
  ```php
  if (is_readable("example.txt")) {
      echo "File is readable";
  } else {
      echo "File is not readable";
  }
  ```

- **is_writable()**: Tells whether the filename is writable.
  ```php
  if (is_writable("example.txt")) {
      echo "File is writable";
  } else {
      echo "File is not writable";
  }
  ```

### File Permissions

#### 6. **Changing File Permissions**

- **chmod()**: Changes file mode.
  ```php
  chmod("example.txt", 0755); // Changes the file permissions to 755
  ```

### File Deletion

#### 7. **Deleting Files**

- **unlink()**: Deletes a file.
  ```php
  if (unlink("example.txt")) {
      echo "File deleted";
  } else {
      echo "File could not be deleted";
  }
  ```

### File Uploads

#### 8. **Handling File Uploads**

- **move_uploaded_file()**: Moves an uploaded file to a new location.
  ```php
  if (move_uploaded_file($_FILES["file"]["tmp_name"], "uploads/" . $_FILES["file"]["name"])) {
      echo "File uploaded successfully";
  } else {
      echo "File upload failed";
  }
  ```

### Directory Operations

#### 9. **Creating and Removing Directories**

- **mkdir()**: Creates a directory.
  ```php
  if (mkdir("new_directory")) {
      echo "Directory created";
  } else {
      echo "Failed to create directory";
  }
  ```

- **rmdir()**: Removes a directory.
  ```php
  if (rmdir("new_directory")) {
      echo "Directory removed";
  } else {
      echo "Failed to remove directory";
  }
  ```

#### 10. **Reading Directories**

- **scandir()**: Lists files and directories inside the specified path.
  ```php
  $files = scandir("uploads");
  print_r($files); // Outputs: Array ( [0] => . [1] => .. [2] => file1.txt [3] => file2.txt )
  ```

- **opendir(), readdir(), closedir()**: Opens, reads, and closes a directory handle.
  ```php
  if ($handle = opendir("uploads")) {
      while (false !== ($entry = readdir($handle))) {
          echo "$entry\n";
      }
      closedir($handle);
  }
  ```

### File Locking

#### 11. **Locking Files**

- **flock()**: Portable advisory file locking.
  ```php
  $file = fopen("example.txt", "r+");
  if (flock($file, LOCK_EX)) { // Acquire an exclusive lock
      fwrite($file, "Add this text");
      flock($file, LOCK_UN); // Release the lock
  } else {
      echo "Could not lock the file";
  }
  fclose($file);
  ```

  ## Practice CLI APP
```php
<?php
$random = rand(1, 10);

do {
    echo "Guess the number(1-10): ";
    $guess = intval(fgets(STDIN));

    if($guess>$random) {
        echo "Too high\n";
    } else if($guess < $random) {
        echo "Too Low\n";
    }
} while($guess!=$random);

echo "Congrats!!!You guessed right\n";
```