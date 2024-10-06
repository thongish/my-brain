```js
function add(n1,n2) {
	return n1 + n2;
};
// Directly invoking the function
add(5, 4);
```

```js
function add(n1,n2) {
	return n1 + n2;
};
// indirectly invoking the function

const refOne = add; // this line causes variable refOne point to the add function

console.log(refOne(3, 7));

const refTwo = add;

console.log(refTwo(9,8));
```

```js
function add(n1,n2) {
	return n1 + n2;
};

function addTwo(num1, addReference) { 
	// higher order function
	// a function that takes a function as a parameter

	return addReference(num1, 2); 
	// calling addReference() which is pointing to the add function
	// this is called a callback function 
}

addTwo(7, add); 
/*
sending add function as an argument to addReference parameter in addTwo function

we are indirectly invoking the add function here
*/
```
### Another example
```js
function calculate(n1, n2, operation) {
	return operation(n1,n2); 
	// you can control the operation you want to perform in this function
	// example if you had a subtract, multiply, divide funciton as well you could send those into this function 
}

calculate(5, 4, add);

function add(n1,n2) {
	return n1 + n2;
};
```

```js
function addTwo(num1, addReference) { 
	return addReference(num1, 2); 
}

addTwo(7, (n1, n2) => { 
	return n1 + n2; 
});
// you can pass an entire function as an argument to a function
```

```js
const colors = ["blue", "red"];

colors.forEach((value, index) => {
	console.log(value, index);
});
// .forEach() is a higher order function, takes a function as the parameter
```

### Practice making our own forEach function
```js
const colors = ["red", "blue"];

function forEach(list, callback) {
    // some looping logic
    for (let i = 0; i < list.length; i++) {
        const color = list[i];
        callback(color, i); // callback inserting the color value and the iteration count (index)
    }
};
// should be no printing inside higher order functions
forEach(colors, (value, index) => {
    console.log(value, index); 
}) // sending function that takes prints value and index
```
### Practice my solution
```js
// Create a function that multiplies two numbers together
/* 
function should be called multiplier and has 3 parameters:
	n1 (MUST BE INTEGER)
	n2 (MUST BE INTEGER)
	callback // should have parameters:
		err
		result
*/
function multiplier(n1, n2, callback) {
    const errorMsg = "This is a number";

    if (typeof n1 == "number" && typeof n2 == "number") {
        const result = Math.round(n1) * Math.round(n2); // can use parseInt() here
        callback(errorMsg, result);
    } else {
        const result = null
        const errorMsg = "This is not a number";
        callback(errorMsg, result);
    }
}

multiplier("5", 5, (err, result) => {
    console.log(err, result);
})
```

### Practice Armaan solution
```js
function multiplier(n1, n2, callback) {
    // logic goes here
    if (typeof n1 != "number" || typeof n2 != "number") {
        // error case
        callback(new Error("Not a valid number"), null);
    } else {
        // success case
        callback(null, parseInt(n1) * parseInt(n2));
    }
}

multiplier("5", 5, (err, result) => {
    // printing goes here
    if (err) {
        console.log(err);
	    return; // will kick us out of the function
	}
	console.log(result); // this won't ever run if err is true
});
```

```js
const fs = require("fs");

const data = fs.readFile("file.txt", (err, data) => {
	console.log(data.toString());
});
// .readFile() is an asynchronous function, which means this function is sent to another thread to finish running

console.log("sending activation email");
```