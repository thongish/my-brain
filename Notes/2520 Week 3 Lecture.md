# Armaan's solution to Lab 2

```js
// mathHelpers.js
const squareRoot = (n) => Math.sqrt(n);
const square = (n) => n * n;
const distance = (n) => {
	return squareRoot(square(n3 - n1) + square(n4 - n2))
}
```

```js
//main.js
const fs = require("fs");
const mathHelpers = require("./mathHelpers");
const { argv } = require("process");
const [, , x1, y1, x2, y2] = argv; // leave first two empty to ignore first two index

// a function called processInput receiving userInput
const processInput = ("${x1}", "${y1}", "${x2}" ,"${y2}") => {

}
// create a directory called dataPoints
	// create a file called points.txt, write userInput into it
	// print a content saved message
	// append the distance message to the end of the file


```