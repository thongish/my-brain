#WEB/W1 

# Comments and semicolon

```
/* Multiline comments start with slash-star,
   and end with star-slash */

// single line comments look like this

// Statements can be terminated by a semicolon ;
var abc;
```

# Typeof operator

```
typeof 20 . // "number"

typeof "Armaan"  // "string"

typeof true  // "boolean"

typeof undefined  // "undefined"

typeof { name: "34" }  "object"

typeof null  // "object" <- this is a bug from 20 years ago

typeof [1, 2, 3]  // "object"
```

# Numbers, Strings, Operators

```
// We can represent numbers in Javascript through the Number type. This type
// includes integers (-1, 0, 1, 2) and floating point numbers (1.5, 4.2, 40.0)

3; // = 3
1.5; // = 1.5

// Some basic arithmetic works as you'd expect.
1 + 1; // = 2

// Ask your Math teacher about floating point precision if you are curious
// why it is not 0.3.
0.1 + 0.2; // = 0.30000000000000004 
8 - 1; // = 7
10 * 2; // = 20
35 / 5; // = 7

// Uneven division is possible too.
5 / 2; // = 2.5

// And mod operator division to get the remainder.
10 % 2; // = 0
30 % 4; // = 2

// Evaluation order priority can be controlled with parentheses.
(1 + 3) * 2; // = 8

NaN; 
// result of e.g. hi/2, stands for 'Not a Number'. This is not a
// seperate data type. It is part of Number type. 

// There's also a boolean type.
true;
false;

// Strings are created with either single ' or double " quotes.
'abc';
"Hello, world";

// I don't mind whether you choose to use single or double quotes for strings
// as long as you are consistent with your choice. 

// Negation uses the ! symbol
!true; // = false
!false; // = true

// Equality (something equals something) is ==
1 == 1; // = true
2 == 1; // = false

// Inequality (something does NOT equal something) is !==
1 != 1; // = false
2 != 1; // = true

// More comparisons
1 < 10; // = true
1 > 10; // = false
2 <= 2; // = true
2 >= 2; // = true

// Strings are concatenated (joined) with +
"Hello " + "world!"; // = "Hello world!"

// ... which works with more than just strings
"1, 2, " + 3; // = "1, 2, 3"

// and are compared with < and >
"a" < "b"; // = true

// Type coercion is performed for comparisons with double equals...
"5" == 5; // = true
null == undefined; // = true

// ...unless you use ===
"5" === 5; // = false
null === undefined; // = false

// Type coercion is a topic we didn't discuss much, but essentially it
// is when Javascript tries to convert a piece of data from one type to
// another. For example: "I want " + 2 + " oranges"; The number is 'coerced'
// (converted) implicitly to a string. We can perform explicit conversion
// from one datatype to anoter using operators like String(2) or Number("32")

// You can access characters in a string with `charAt`
"This is a string".charAt(0);  // = 'T'

// The charAt above essentially says: "give me the 0th character in the string"
// If we do charAt(1), it will give us h (character at index 1). 

// we can use `substring` to get larger pieces out of a string.
"Hello world".substring(0, 5); // = "Hello"

// In substring, the numbers are (INCLUDING, EXCLUDING). This means
// start at character at index 0, and go UP TO (but don't INCLUDE) the
// character at position 5. This means characters at index 0, 1, 2, 3, 4 will
// be pulled out into their own string. 

// `length` is a property, not a fuction, so don't use ().
"Hello".length; // = 5

// There's also `null` and `undefined`.
null;      // used to indicate a deliberate non-value
undefined; // used to indicate a value is not currently present. By default,
// when you define a variable like this: 
var someVar; 
// Javascript will give someVar the value of undefined. 

// false, null, undefined, NaN, 0 and "" are what are known as "falsy"
// values. 
 
// This means if you have the variables like:
var a = false;
var b = null;
var c = undefined;
var d = "";

if (a) {

} else {
// will enter the else
}

if (b) {

} else {
// will enter the else
}

if (c) {

} else {
// will enter the else
}

if (d) {

} else {
// will enter the else
}


// All of those variables will not have a "truthy" value inside them, meaning
// in an if statement, they will be regarded as the same as "false". 

```

# Variables, arrays, and objects

```
// Variables are declared with the `var` keyword. Assignment uses a single `=`
// character.
var someVar = 5;

// In modern javascript, we have access to the let and const keywords. 
let someVar2 = 5;
const someConstant = 3.14;

// When we use var, our variables are only locally scoped within functions. 
// By introducing let or const, we can acheive { } block scoped variables. 

// If it's your first time creating a variable and you leave 
// the var keyword off, you won't get an error...
someOtherVar = 10;

// ...but your variable will be created in the global scope, not in the scope
// you defined it in. This is very dangerous! DON'T DO THIS. 

// Variables declared without being assigned a value as I mentioned earlier
// are set to undefined.
let someThirdVar; // = undefined

// There's shorthand for performing math operations on variables:
someVar += 5; // equivalent to someVar = someVar + 5; someVar is 10 now
someVar *= 10; // now someVar is 100

// and an even-shorter-hand for adding or subtracting 1
someVar++; // now someVar is 101
someVar--; // back to 100

// Arrays are ordered lists of values, of any type.
let myArray = ["Hello", 45, true];

// Their values can be accessed using the square-bracket syntax.
// Array indices start at zero.
myArray[1]; // = 45

// Arrays are MUTABLE
myArray.push("World");
myArray.length; // = 4

// Add/Modify at specific index
myArray[3] = "Hello";

// Add and remove element from front or back end of an array
myArray.unshift(3); // Add as the first element
someVar = myArray.shift(); // Remove first element and return it
myArray.push(3); // Add as the last element
someVar = myArray.pop(); // Remove last element and return it

// Imagine you want to join all elements of an array with dashes
// into 1 big string. You can use .join which returns back to you a string. 
let myArray0 = [32,false,"js",12,56,90];
myArray0.join("-"); // = "32-false-js-12-56-90"

// Get subarray of elements from index 1 (include) to 4 (exclude)
myArray0.slice(1,4); // = [false,"js",12]

// JavaScript's objects are collection of key-value pairs. Each key name
// MUST be unique. The key is on the left of the semicolon: value on the right. 
let myObj = {key1: "value1", key2: "value2"};

// Object attributes can also be accessed using the subscript syntax,
myObj["key1"]; // gives us back "value1"

// ... or using the dot syntax
myObj.key1; // gives us back "value1". 

// Objects are mutable; values can be changed and new keys added.
myObj.key3 = "value3"; // Here we insert a new key-value pair. 

// If you try to access a value that's not yet set, you'll get undefined.
myObj.myFourthKey; // = undefined
```

# Control structures and loops

```
// The `if` statement works as you'd expect.
let count = 1;

if (count == 3){
    // evaluated if count is 3
} else if (count == 4){
    // evaluated if count is 4
} else {
    // evaluated if it's not either 3 or 4
}

// As does `while`.
while (true){
    // An infinite loop!
}

// Do-while loops are like while loops, except they always run at least once.
var input;
do {
    input = getInput();
} while (!isValid(input));

// The `for`:
// initialization; continue condition; iteration.
for (let i = 0; i < 5; i++){
    // will run 5 times
}

// Quick Check to make sure your brain is awake:
// In the for loop above, can we switch the let i = 0; to const i = 0; ?

// The for/in loop allows for looping over an object.

let description = "";

let person = { fname: "Adam", lname: "Siyala", age: 20};

for (let key in person) {
    description += person[key] + " ";
} // description = 'Adam Siyala 20'

// The for/of statement allows iteration over Strings, Arrays, and more. 
// (But not a standard object. For objects, use for in). 

let myPets = "";

let pets = ["cat", "dog", "hamster", "bunny"];

for (let pet of pets){
    myPets += pet + " ";
} // myPets = 'cat dog hamster bunny'

// && is logical and, || is logical or

if (house.size == "big" && house.color == "blue") {
    // both conditions MUST be true to enter this if statement
}
if (color == "red" || color == "blue") {
    // as long as color is either red OR blue, we enter this if block
}

// The `switch` statement
// Use 'break' after each case
// or the cases after the correct one will be executed too.
let grade = 'B';
switch (grade) {
  case 'A':
    console.log("Great job");
    break;
  case 'B':
    console.log("OK job");
    break;
  case 'C':
    console.log("You can do better");
    break;
  default:
    console.log("Oy vey");
    break;
}

```

# Functions and scope in JavaScript

```
// JavaScript functions are declared with the `function` keyword.
function myFunction(thing) {
    return thing.toUpperCase();
}
myFunction("foo"); // = "FOO"

// JavaScript functions are first class objects, so they can be reassigned to
// different variable names and passed to other functions as arguments - for
// example, when supplying an event handler:
function myFunction(){
    // this code will be called in 5 seconds' time
}
setTimeout(myFunction, 5000);

// JavaScript has function scope; functions get their own scope but other blocks
// do not.
if (true){
    var i = 5;
}
console.log(i); // 5...not undefined as you'd expect in a block-scoped language
// We can access the variable i outside the if block because we used var. 

// We can write functions in three ways:

// 1) Function declaraction syntax
function myFunc() {

}

// 2) Function expression syntax
let myFunc() = function() {

}

// 3) Arrow function syntax
let myFunc() = () => {

}

// Be careful about function declaraction syntax. It uses "hoisting". This 
// means you can call the function BEFORE you define it. So:
myFunc();

function myFunc() {

}
// Above is no problem, but:
myFunc()

let myFunc() = function() {

}
// or

let myFunc() = () => {

}

// the above will NOT be okay. No hoisting occurs with expression syntax or
// arrow function syntax. 
```


# [[2520 Week 1]]



# Flash Cards

`"1, 2, " + 3;`
Is this a valid line of code?
?
Yes, you can concatenate a number type with a string type
- this is called Type coercion

`"This is a string".charAt(3)`
What does this line of code return?
?
"s"
- `.charAt()` accesses characters in a string at the specified index

`"5" == 5;` is true. Why?::Double equals comparisons performs Type coercion 

true or false?
`"5" === 5;`
?
false

`"Hello world".substring(0, 5);
What is the output of this line?
?
"Hello"
- The substring method extracts a portion of a string between two indices
	- First index is inclusive
	- Second index is exclusive

`"Hello".length`
`"Hello".length()`
Which one is correct?
?
`"Hello".length`
- `.length` is a property, not a function

Why would you want to use `null`?:: To indicate a deliberate non-value

Why would you want to use `undefined`:: To indicate a value is not currently present

`const someVar;`
This line hasn't given the variable `someVar` a value, what is the default value that is given to this variable?
?
`undefined`

`false`,
`null`,
`undefined`,
`Nan`,
`0`
and `""` 
are known as what values?
?
"falsy" values
-  A value that is considered false when encountered in a Boolean context

Why is this line of code dangerous?
`someVar = 10;`
?
Because without the use of `var` ,  `let`,  or `const`, the variable will be created in the global scope, not the scope you defined it in

```
let someVar = 10;

someVar++;
someVar--;
```
What is the value of `someVar`?
?
10
- `someVar++` and `someVar--` are short-hand for adding or subtracting by 1

```
let myArray = [1, 2, 3, 4];

myArray.unshift(0);
```
What is the value of `myArray`?
?
`[0, 1, 2, 3, 4]`
- `.unshift()` Adds to to an array as the first element

```
let myArray = [1, 2, 3, 4];

someVar = myArray.shift();
```
What is the value of `someVar`?
?
1
- `.shift()` removes the first element and returns it


```
let myArray = [1, 2, 3, 4];

someVar = myArray.pop();
```
What is the value of `someVar`?
?
4
- `.pop()` removes the last element and returns it

```
let myArray0 = [32,false,"js",12,56,90];

console.log(myArray0.join("-"));
```
What is the output of this code snippet?
?
`"32-false-js-12-56-90"`
- `.join()` method returns a new string by concatenating all elements in an array, separated by commas or a specified separator string
	- in this case, the separator string is `"-"`

```
let myArray0 = [32,false,"js",12,56,90];

console.log(myArray0.slice(1,4));
```
What is the output of this code snippet?
?
`[false,"js",12]`
- `.slice()` method extracts a portion of an array between two indices
	- First index is inclusive
	- Second index is exclusive

```
let myObj = {
	key: "value1",
	key: "value2",
};
```
Is this a valid JavaScript object?
?
No, the keys in a JavaScript object MUST be unique

```
let myObj = {
	key1: "value1",
	key2: "value2",
};

myObj[key1];

myObj.key1;
```
Which of the two accessing methods is correct in this code snippet?
?
Both are valid ways to access the value of `key1`

```
let myObj = {
	key1: "value1",
	key2: "value2",
};
```
How would you add a new key-value pair to this object?
?
`myObj.key3 = "value3"`
- Despite being able to access key values with subscript syntax `myObj[key2]`, you can't change or add new keys with it

```
for (let i = 0; i < 5; i++){
	console.log(i)
};
```
How many times will this for loop run?
?
5

```
let description = "";

let person = { fname: "Adam", lname: "Siyala", age: 20};

for (let key in person) {
    description += person[key] + " ";
};
```
What is the value of `description`?
?
`'Adam Siyala 20'`
- the for/in loop allows for looping over an object

```
let myPets = "";

let pets = ["cat", "dog", "hamster", "bunny"];

for (let pet of pets){
    myPets += pet + " ";
};
```
What is the value of `myPets`?
?
`'cat dog hamster bunny'`
- the for/of loop allows for looping over strings, arrays, and more

```
let house = {
	size: "big",
	color: "red",
};

if (house.size == "big" && house.color == "blue") {
	console.log("Big blue house");
};
```
Does `console.log("Big blue house")` run here?
?
No, the `&&` is a logical `and` operator

```
let house = {
	size: "big",
	color: "red",
};

if (house.size == "big" || house.color == "blue") {
	console.log("Big blue house");
};
```
Does `console.log("Big blue house")` run here?
?
Yes, the `||` is a logical `or` operator

```
let grade = 'B';
switch (grade) {
  case 'A':
    console.log("Great job");
    break;
  case 'B':
    console.log("OK job");
    break;
  case 'C':
    console.log("You can do better");
    break;
  default:
    console.log("Oy vey");
    break;
}
```
What will be printed in the terminal?
?
`"OK job"`
- Remember to use `break` after each case, or the cases after the correct one will be executed too

How do you declare a JavaScript function?
?
Using the `function` keyword
```
function myFunction() {
    
}
```

```
function myFunc() {

}
```
What kind of function syntax is this?
?
Function declaration syntax

```
let myFunc() = function() {

}
```
What kind of function syntax is this?
?
Function expression syntax

```
let myFunc() = () => {

}
```
What kind of function syntax is this?
?
Arrow function syntax

```
myFunc();

function myFunc() {

}
```
Will this piece of code run?
?
Yes, because function declaration syntax allows for hoisting, which means you can call the function BEFORE you define it











