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

### Statements

You have seen some statements already:

```javascript
print "Hello World!";
```

Lox also have a special type of statement called expression statement. It is basically an expression followed by a semicolon.

```javascript
"Hello World!";
```

You can group statements in a block, but this will effect the scope of variables which will be discussed later.

```javascript
{
    print "Hello World! 1";
    print "Hello World! 2";
}
```

### Variables

You declare variables using <code>var</code> statements. If you omit the initializer, the variable’s value defaults to <code>nil</code>:

```javascript
var imAVariable = "here is my value";
var iAmNil;
```

You can use variables in function calls and statements after defining:

```javascript
var breakfast = "bagels";
print breakfast; // "bagels".
breakfast = "beignets";
print breakfast; // "beignets"
```

### Control Flow

An if statement executes one of two statements based on some condition:

```javascript
if (condition) {
  print "yes";
} else {
  print "no";
}
```

A while loop executes the body repeatedly as long as the condition expression evaluates to true:

```javascript
var a = 1;
while (a < 10) {
  print a;
  a = a + 1;
}
```

Finally, we have for loops:

```javascript
for (var a = 1; a < 10; a = a + 1) {
  print a;
}
```

### Functions

A function call expression looks the same as it does in C:

```javascript
makeBreakfast(bacon, eggs, toast);
```

You can also call a function without passing anything to it:

```javascript
makeBreakfast();
```

In Lox, you declare your own functions with fun:

```javascript
fun printSum(a, b) {
  print a + b;
}
```

The body of a function is always a block. Inside it, you can return a value using a return statement:

```javascript
fun returnSum(a, b) {
  return a + b;
}
```

If execution reaches the end of the block without hitting a <code>return,</code> it implicitly returns <code>nil</code>.

#### Closures

Functions are first class in Lox, which just means they are real values that you can get a reference to, store in variables, pass around, etc. This works:

```javascript
fun addPair(a, b) {
  return a + b;
}

fun identity(a) {
  return a;
}

print identity(addPair)(1, 2); // Prints "3".
```

Since function declarations are statements, you can declare local functions inside another function:

```javascript
fun outerFunction() {
  fun localFunction() {
    print "I'm local!";
  }

  localFunction();
}
```

If you combine local functions, first-class functions, and block scope, you run into this interesting situation:

```javascript
fun returnFunction() {
  var outside = "outside";

  fun inner() {
    print outside;
  }

  return inner;
}

var fn = returnFunction();
fn();
```

### Classes

```java
class Breakfast {
  cook() {
    print "Eggs a-fryin'!";
  }

  serve(who) {
    print "Enjoy your breakfast, " + who + ".";
  }
}

// Store it in variables.
var someVariable = Breakfast;

// Pass it to functions.
someFunction(Breakfast);

var breakfast = Breakfast();
print breakfast; // "Breakfast instance".
```

#### Instantiation & Initialization

```java
breakfast.meat = "sausage";
breakfast.bread = "sourdough";
```

Assigning to a field creates it if it doesn’t already exist.

If you want to access a field or method on the current object from within a method, you use good old this:

```java
class Breakfast {
  serve(who) {
    print "Enjoy your " + this.meat + " and " +
        this.bread + ", " + who + ".";
  }

  // ...
}
```

Part of encapsulating data within an object is ensuring the object is in a valid state when it’s created. To do that, you can define an initializer. If your class has a method named init(), it is called automatically when the object is constructed. Any parameters passed to the class are forwarded to its initializer:

```java
class Breakfast {
  init(meat, bread) {
    this.meat = meat;
    this.bread = bread;
  }

  // ...
}

var baconAndToast = Breakfast("bacon", "toast");
baconAndToast.serve("Dear Reader");
// "Enjoy your bacon and toast, Dear Reader."
```

#### Inheritance

```java
class Brunch < Breakfast {
  drink() {
    print "How about a Bloody Mary?";
  }
}
```

Here, Brunch is the derived class or subclass, and Breakfast is the base class or superclass. Every method defined in the superclass is also available to its subclasses:

```java
var benedict = Brunch("ham", "English muffin");
benedict.serve("Noble Reader");
```

As in Java, you can use super:

```java
class Brunch < Breakfast {
  init(meat, bread, drink) {
    super.init(meat, bread);
    this.drink = drink;
  }
}
```
