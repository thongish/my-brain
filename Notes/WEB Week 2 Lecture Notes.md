#WEB/W2

```js
// Let's make a simple add function and invoke it (call the function)
function add (num1, num2) {
	return num1 + num2;
}

add(4,5);


// This is not the only way we can invoke the add function, we can also indirectly
// invoke it using a reference. 

const referenceOne = add;
referenceOne(3,7);

const referenceTwo = add;
referenceTwo(9,8);

// Let's now make things a tiny bit more complicated

function addTwo(num1, addReference) {
	return addReference(num1, 2);
} 

addTwo(7, add);

// the function that we are passing in to the addTwo function(add) is called a
// callback function

// the addTwo function itself is known as a higher order function


// So far, everything we have seen has NOT been asynchronous. Callbacks in 
// javascript do NOT only apply to async code.

// The forEach function, which we call on an array
// 1 - Give it a callback function
// 2 - Callback will take as first argument the itemInList, second is index

function callback(itemInList, index) {
	console.log(itemInList + " is at position " + index);
  // Sidenote: we can write this also as
  console.log(`${itemInList} is at position ${index}`);
}

array.forEach(callback);

// How you will see things in the wild (with the function written directly in)
// We call this an anonymous function when we write the function directly in

array.forEach(function(itemInList, index) {
	console.log(itemInList + " is at position " + index);
  // Sidenote: we can write this also as
  console.log(`${itemInList} is at position ${index}`);
});

// So forEach is an example of a higher order function. It takes in a callback 
// that it will call for us, with each item in the array. How can we create
// our own version of forEach?

// our own forEach implementation
function forEach(list, callback) {
	for (let i = 0; i < list.length; i++) {
		callback(list[i], i);	
	}
}

let arrayOfNums = [1,2,3,4,5];

function callbackFunc(listItem, listPosition) {
	console.log(`${listItem} is at index ${listPosition}`);
}
// call out forEach function, giving it an array and a callback to call
forEach(arrayOfNums, callbackFunc);

// Most typically, when you use callbacks, what we are trying to do is
// defer execution of a function to a later point in time. You will
// often see in browser-side javascript, callbacks are used for event
// listeners. I don't know when a user will click, but I know what function
// I want to run when they eventually DO click.


//Create a function called multiplier which takes 3 arguments:
// number1
// number2
// callback

// callback contains 2 parameters
// err
// result

// number1 and number2 must be Integers. If decimals are passed, convert them

// If the user passes in for number1 or number2 something which IS NOT a
// number, pass an error to the first argument, and leave result empty. 

// Otherwise, multiply the two numbers together and pass null for the error,
// result as the second argument. 

// Wrap all of this in a setTimeout which will execute after 4 seconds.  

// Sample Solution
function multiplier(number1, number2, callback) {
  setTimeout(() => {
    if (typeof number1 !== 'number' || typeof number2 !== 'number') {
      callback(new Error('the first and second arguments must be number'));
    } else {
      const result = parseInt(number1) * parseInt(number2);
      callback(null, result);
      }
  }, 4000);
}

multiplier(3, 4, function(err, result) {
	if(err) {
		console.log(err);
	} else {
		console.log(result);
	}
});

// This is fine, but first, the error is looking a little clunky. I just want
// the error message I passed in to show. Nothing else. How can I control this?

// I can actually do err.message since Error is an object with a message key
multiplier(3, 4, function(err, result) {
	if(err) {
		console.log(err.message);
	} else {
		console.log(result);
	}
});

// This pattern of passing an error first is called error-first callbacks
// It is a convention in Node

// Let's see an example of this with the fs module

const fs = require("fs");

function callback(err) {
	if(err) {
		console.log(err);
	} else {
		console.log("Your file was saved correctly");
	}
}

fs.writeFile("myfile.txt", "hello world", callback);

// What can we improve here
// 2 small optimizations we can make to reduce the busy-ness of our code
// 0) Use an anonymous function
// 1) Convert to an arrow function (node official docs use this)
// 2) get rid of the else and simply add a return to the first console

// Anon func
const fs = require("fs");
fs.writeFile("myfile.txt", "hello world", function(err) {
	if(err) {
		console.log(err);
	} else {
		console.log("Your file was saved correctly");
	}
});

// step 1 and 2
const fs = require("fs");
fs.writeFile("myfile.txt", "hello world", (err) => {
	if(err) {
		return console.log(err);
	}
		console.log("Your file was saved correctly");
});
```


# Flash cards

```js
function add (num1, num2) {
	return num1 + num2;
}
//
function addTwo(num1, addReference) {
	return addReference(num1, 2);
}
//
addTwo(7, add);
```
What is `{js}addTwo(7, add);` doing?
?
It is calling the function `{js}addTwo()` and passing in a number and the function `{js}add()`
- What's happening is it takes the number `{js}7` and uses the `{js}add()` as a callback function to add `{js}2` to it

What is a **higher order function**?::A function that takes a function as an argument 

