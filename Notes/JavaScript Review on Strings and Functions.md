#WEB/W1
# Functions 

- **Hierarchical function call** or **nested function call**
	- When you call a function or multiple functions within a function
- Functions generally should do just one thing
	- If a function does more than one thing, it should be "decomposed" into two or more functions

#### Negative one (-1)

- Common in programming for a function or method to return -1 when a search term is not found
- This is a convention

## Built-in JavaScript functions

- `{js}Number(value)` - accepts a value and converts it to a number
- `{js}String(value)` - accepts a value and converts it to a string
- `{js}isFinite(number)` - accepts a value and returns false if it is:
	- `{js}+Infinity`,
	- `{js}-Infinity`,
	- `{js}NaN`
- `{js}isNaN(number)` - returns false if the argument passed tot he function is not a number
- `{js}parseFloat(string)` - parses a string and returns a floating point number
- `{js}parseInt(string)` - parses a string and returns an integer (whole number)

# Strings

- A **string** is a sequence (or string) of text characters we can store in a variable
- A **string literal** is the value of a string
	- `{js}"This is a string literal"`

- `{js}'My mom's car is faster than my car'`
	- This string is wonky as you can see
	- Can fix using backslash
		- `{js}'My mom\'s car is faster than my car'`

- Invoking string methods such as `{js}string.toUpperCase()` or `{js}string.toLowerCase()` does not change the original string
 ![[Pasted image 20240909202817.png]]

#### Can we compare strings?

- Strings are sorted lexicographically (alphabetical kinda)
- Every character in a string is part of the Unicode character set, and each Unicode character has a **code point**
	- JavaScript compares strings using the code point
```js
var a = 'a';  
var b = 'b’;  
if (a < b) {  
	console.log(a + ' is less than ' + b);  
} else if (a > b) {  
	console.log(a + ' is greater than ' + b);  
} else {  
	console.log(a + ' and ' + b + ' are equal.');  
}
```
## ASCII and Unicode

-  Strings use **character sets**
	- A character set is an ordered list (sequence) of characters
	- Each character in the list has a unique number (index)
	- A string in JavaScript can contain any character from the **Unicode** character set

- JavaScript uses Unicode to represent every possible character as a unique integer, known as **code point**
	- i.e. the character "A" has the code point value of 65
- Sometimes converting between a text character and the encoded code point integer is useful
	- You can do this with the function `{js}string.codePointAt()`

# Scope

#### Global variables

- Defined outside of a function
- Scope extends from from its assignment statemen to the **end of the file**

#### Local variables

- Defined inside a function or block
- Scope is limited to inside its function or block

# readline-sync

- Node module that allows getting input from the user in the terminal
- Important that we clean the input data before doing anything with it
	- i.e. trim whitespace, make sure it's in the right case, etc.
```js
const cmPerInch = 2.54;
const inchesPerFoot = 12;
const readline = require('readline-sync');

var feet = readline.question("How tall are you in feet (omit inches): ");
var inches = readline.question("Enter omitted inches: ");
var totalInches = feet * inchesPerFoot + inches;
var totalCM = totalInches * cmPerInch;

console.log('Centimeters: %f\n', totalCM);
```
- The output from this code snippet is completely unexpected because the user inputs are stored as strings and not numbers

- To fix this piece of code, we would have to convert the values into numbers first like so:
```js
const cmPerInch = 2.54;
const inchesPerFoot = 12;
const readline = require('readline-sync');

var feet = parseInt(readline.question("How tall are you in feet (omit inches): "));
var inches = parseInt(readline.question("Enter omitted inches: "));
var totalInches = feet * inchesPerFoot + inches;
var totalCM = totalInches * cmPerInch;

console.log('Centimeters: %f\n', totalCM);
```




# Flash cards

What is a hierarchical function call in programming?::When you call a function or multiple functions within a function.
<!--SR:!2024-09-29,1,210-->

How should functions generally be designed?::Functions should generally do just one thing; if a function does more than one thing, it should be decomposed into two or more functions.
<!--SR:!2024-10-25,15,230-->

What is the convention for a function or method returning -1?::It commonly indicates that a search term was not found.
<!--SR:!2024-09-29,1,190-->

What does the `{js}Number(value)` function do in JavaScript?::It converts the value to a number.
<!--SR:!2024-10-11,13,270-->

What does the `{js}String(value)` function do in JavaScript?::It converts the value to a string.
<!--SR:!2024-10-11,13,270-->

What does the `{js}isFinite(number)` function do in JavaScript?::It returns false if the number is `Infinity`, `-Infinity`, or `NaN`.
<!--SR:!2024-09-30,2,250-->

What does the `{js}isNaN(number)` function do in JavaScript?::It returns false if the argument is not a number.
<!--SR:!2024-09-30,2,230-->

What does the `{js}parseFloat(string)` function do in JavaScript?::It parses a string and returns a floating-point number.
<!--SR:!2024-10-11,13,270-->

What does the `{js}parseInt(string)` function do in JavaScript?::It parses a string and returns an integer.
<!--SR:!2024-10-17,19,250-->

What is a string in JavaScript?::A sequence of text characters that can be stored in a variable.
<!--SR:!2024-10-18,20,250-->

What is a string literal in JavaScript?::The value of a string, e.g., `{js}"This is a string literal"`.
<!--SR:!2024-10-17,19,250-->

How can you fix a string containing a single quote in JavaScript?::Use a backslash to escape the single quote, e.g., `{js}'My mom\'s car is faster than my car'`.
<!--SR:!2024-10-18,20,250-->

Do string methods like `{js}string.toUpperCase()` change the original string?::No, they do not change the original string.
<!--SR:!2024-10-07,9,250-->

How are strings compared in JavaScript?::Strings are compared lexicographically based on Unicode code points.
<!--SR:!2024-09-29,1,210-->

What is Unicode in JavaScript?::A character set that represents every possible character with a unique integer known as a code point.
<!--SR:!2024-09-29,1,190-->

How can you convert a text character to its Unicode code point in JavaScript?::Use the function `{js}string.codePointAt()`.
<!--SR:!2024-10-07,9,250-->

What is the scope of global variables in JavaScript?::Global variables are defined outside of a function and extend from their assignment statement to the end of the file.
<!--SR:!2024-10-17,19,250-->

What is the scope of local variables in JavaScript?::Local variables are defined inside a function or block and are limited to inside that function or block.
<!--SR:!2024-10-02,4,230-->

What is the `{js}readline-sync` Node module used for?::It allows getting input from the user in the terminal.
<!--SR:!2024-11-02,23,250-->

Why should you clean input data when using `{js}readline-sync`?::To ensure the data is in the correct format, such as trimming whitespace and converting to the right case.
<!--SR:!2024-09-29,1,210-->

How do you convert user input from `{js}readline-sync` to numbers in JavaScript?::Use `{js}parseInt()` or `{js}parseFloat()` to convert the string inputs to numbers.
<!--SR:!2024-10-21,11,230-->