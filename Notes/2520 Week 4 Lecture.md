```js
const fs = require("node:fs");

function readFileP(filename) {
	fs.readFile(filename, "utf8", (err, data) => {
	if (err) {
		console.log(err);
	} else {
		console.log(data);
	}
	})
}
```

# Promises

- A state machine
- Promise can be in any 3 states at any single time
	- Pending
	- Fulfilled
	- Rejected
- We are the ones responsible for figuring out when the states transition
- Promise can only be in one state at a time

- whenever inside a .then() javascript is going to automatically wrap the output in a promise object

- lab going to ask to do a bunch of file stuff
	- wrap everything into promises
	- import util module
		- util.promisify(fs.readFile) converts function to version that works with promises
	- const fs = require("node:fs/promises"); turns all functions in fs into a promise

- 

order of testing by armaan
- register
- create a blog
- create post
- register another user
- user 2 will like user 1 post (run multiple times maybe)
- after running these steps, should see in our project file 
#### Google this

- Callback hell
- Luhn's Algorithm