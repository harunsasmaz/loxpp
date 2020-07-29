# Lox++

A C++ Implementation of Lox language

For more details about Lox, please check [Crafting Interpreters Book Website](https://craftinginterpreters.com/).

Also, there is a repository of the book mentioned above, you can visit [here](https://github.com/munificent/craftinginterpreters).

## Compile & Run

```bash
$ cmake .
$ make
$ ./loxpp samples/fib.lox
```

## Lox Language

### Hello Lox

Classic introduction to the language; here is your very first program:

```c
print "Hello World!";
```

### Data Types

#### Booleans

There are two Boolean values, obviously, and a literal for each one:

```c
true;
false;
```

#### Numbers

Lox only has one kind of number: double-precision floating point. For simplicity, it only supports integers and decimal numbers.

```c
1234;
12.34;
```

#### Strings

Like most languages, strings are enclosed in double quotes:

```c
"I am a string";
"";    // The empty string.
"123"; // This is a string, not a number
```

#### Nil

The representation of "no value", NULL, like many other languages have.

### Expressions

#### Arithmetic

Lox supports basic arithmetic operations as they common in all languages;

```c
add + me;
subtract - me;
multiply * me;
divide / me;
-negateMe;
```

All operations are applicable on numeric values, except addition. You can <b>concatanate two strings</b> with addition operation.

#### Comparison & Equality

You can compare different types of values, not restricted to numbers. 

```c
less < than;
lessThan <= orEqual;
greater > than;
greaterThan >= orEqual;
equal == than;
not != equal;
```

You can compare strings;

```c
"cat" != "dog"; // true.
```

Or even a string with a number;

```c
123 == "123"; // false.
```

#### Logical Operators

```c
!true;  // false.
!false; // true.
```

```c
true and false; // false.
true and true;  // true.
```

```c
false or false; // false.
true or false;  // true.
```

#### Precedence & Grouping

You can group stuff to ensure correct precedence that you want to see:

```javascript
var average = (min + max) / 2;
```
