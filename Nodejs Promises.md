#WEB/W4

# Creating a promise object

```js
const myPromise = new Promise();
```

- A promise is an object that contains a status (PromiseStatus) and a value (PromiseValue)
- The value of the **PromiseStatus** can be one of three values:
	- fulfilled - Promise has been **resolved**
		- Everything went fine, no errors occurred within the promise
	- rejected - Promise has been **rejected**
		- Something went wrong
	- pending - Neither **resolved** or **rejected**, the promise is still **pending**

- Takes a function which takes two functions as parameters
- There will be a condition in the function.
	- If the condition is met, the promise will be resolved, otherwise rejected
```js
const myPromise = new Promise((resolve, reject) => {  
    let condition;  
    
    if(condition is met) {    
        resolve('Promise is resolved successfully.');  
    } else {    
        reject('Promise is rejected');  
    }
});
```

- Attach a `then` for resolve, and a `catch` for reject
```js
myPromise
	.then((message) => { console.log(message);})
	.catch((message) => { console.log(message);
	});
```


# Armaan stuff

```js
Questions we want to answer: 
1) How do we create a promise
2) How do we change the status of the promise
3) How do we listen for when the status of a promise changes
*/

// (1) Simple way to create a promise
let promise = new Promise();

// (2) How do you change the state of the promise
let promise = new Promise();
// We give the promise a single callback function, that takes in two 
// functions, resolve and reject

// When you call resolve(), the status changes to fulfilled
// When you call reject(), the status changes to rejected

let promise = new Promise((resolve, reject) => {
	resolve()  // promise is fulfilled
	reject()  //  promise is rejected
});

// Let's take a look at what a promise is exactly

// Open chrome dev tools and write the following below
let promise = new Promise((resolve, reject) => {
});

console.log(promise);

// Notice it's just an object. 
// Now we have a special thing call proto, which basically is a bunch
// of hidden methods we can call on this object. We are interested in 
// then and catch

// When a promise state changes to fulfilled (which happens when we call resolve)
// the function that we pass to "then" will be called. 

// When a promise state changes to rejected (which happens when we call reject)
// the function that we pass to "catch" will be called

// Time for you to test things out==================================

// Create two functions, onResolved and onRejected. Inside each function, 
// console.log "success" and "error" respectively. 


// Create a new promise, which takes a function contained resolve and reject
// as parameters. In the function body, timeout for 3 seconds, then call
// resolve(). Now make another promise, which takes again a resolve and reject,
// but this time call reject. Again, timeout for 3 seconds. Do this in chrome
// devtools. 

// finally, call .then() and .catch() on your promise, passing your
// onResolved and onRejected parameters respectively. 

// Sample Solution
function onResolved() {
	console.log("success");
}

function onRejected() {
	console.log("error");
}

var promise = new Promise((resolve, reject) => {
	setTimeout(() => {
	resolve() //fulfilled
	}, 3000)
});

promise
.then(onResolved)
.catch(onRejected);

// We create a promise. After 3 seconds, it calls resolve. This means
// our .then will trigger, calling our onResolved function. 

// if we call reject() instead of resolve, our onRejected will be called. 


// Let's now do some practice with Node.js and promises

// Try and convert fs.readFile() into a promise. It uses a callback by default
// call your function  

// call your function readFilePromise

// Sample Solution
function readFilePromise(filename) {
    return new Promise(function(resolve, reject) {
        fs.readFile(filename, function(err, data){
            if (err) 
                reject(err); 
            else 
                resolve(data);
        });
    });
};

// small note: we can also write our function like so

let readFilePromise = function(filename) {
    return new Promise(function(resolve, reject) {
        fs.readFile(filename, function(err, data){
            if (err) 
                reject(err); 
            else 
                resolve(data);
        });
    });
};

// one interesting advantage of this syntax is that I can easily refactor
// it to do something really interesting. I can make it part of the fs module.

fs.readFilePromise = function(filename) {
    return new Promise(function(resolve, reject) {
        fs.readFile(filename, function(err, data){
            if (err) 
                reject(err); 
            else 
                resolve(data);
        });
    });
};


// Remember the issues we had with callbacks earlier? 
// - Hard to read
// - no centralized error handling

// You can see how we fixed both these issues 

//===============================================================
// Recall what we had earlier
function multiplier(number1, number2, callback) {
    if (typeof number1 !== 'number' || typeof number2 !== 'number') 
      callback(new Error('the first and second arguments must be number'));
      const result = parseInt(number1) * parseInt(number2);
      callback(null, result);
}

multiplier(3, 4, function(err, result) {
	if(err) {
		console.log(err);
	} else {
		console.log(result);
	}
});

// Try and convert this into a Promise

// Sample Solution
function multiplier(number1, number2) {
  return new Promise((resolve, reject) => {
    if (typeof number1 !== 'number' || typeof number2 !== 'number') 
      reject(new Error('the first and second arguments must be number'));
      const result = parseInt(number1) * parseInt(number2);
      resolve(result);
  });
}

// Actually calling our function and dealing with the promise

// .then, gets the result
multiplier(1, 2).then(data => {
  // now data is 1 * 2 = 2
  // ...
});
// .catch, catchs the error
multiplier(1, 'a').catch(error => {
  // now the error is about the fact that 'a' is not a number
  // ...
});
```