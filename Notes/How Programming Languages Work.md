#WEB/W1

[Matthew's Notes](https://docs.google.com/document/d/1JYqZjQik9nlr-2aGGN8kjb1KHhAZ-y7ST4R7-gjAF0A/edit)
# **Compiler** 

- translates source code to assembly, reads entire source code before sending it off to the CPU
- If errors in source code, program will not run at all
- will always be faster than interpreter because code is translated in advance rather than code being shipped bundled with interpreter

# **Interpreter** 

- reads and runs source code line by line. will stop program if it runs into an error
- is python a compiled language or interpreted language?
	- combination of both
	- modern python/PHP/node.js/etc. actually do have compilers called JIT compiler
# **Pure Function** 

- function where given a set of inputs the function returns the same output every time
	- if interpreter sees any pure functions, that piece of code is sent to the JIT compiler (cached) aka compiled in advance stored in a .pyc file

# **Languages a browser can understand:**

1. **HTML** - responsible for content + layout
2. **CSS** - makes your content look stylish
3. **JavaScript** - controls behavior i.e.. when user performs an "action" like clicking a button
	- language that lives in the browser
	- runtime environment is the browser itself
	- only programming language in the world that can run without users installing a runtime environment
	- V8 engine (interpreter)
	- ECMA-262, ECMA script - everything JavaScript is capable of doing
	- very limited capability because safety sandbox

# **What does it take to create a program and run it on a computer?**

1. Programming language i.e.. Ruby, Python, Java
2. Runtime environment
	- collection of things bundled together
	- compiler or interpreter
	- provide extra facilities to help your programming language interact with its environment
		- APIs, pieces of code that have been written already and influences how the programming language interacts with the environment
		- example, Java Microphone Library
			- can now use microphone.turnon
	- exact same programming language will run entirely different depending on what runtime environment it is being run from
	- every programming language needs a runtime environment in order to execute (work)

# **Node.js**

- uses JavaScript programming language
- a runtime environment
- keeps V8 engine
- doesn't keep web APIs instead introduces Node.js API's
- way for JavaScript to be executed outside of the browser, can talk directly with PC
- can run JavaScript on the front-end and back-end

# **Object Destructuring**


# [[2520 Week 1]]



# Flash Cards

What does a compiler do?
?
Translates source code into machine/binary language
- Necessary to make a program executable

Compiler or interpreter, which is faster?
?
Compiler
- Will always be faster because entire code base is translated in advance rather than code being read line by line upon execution

What is a Pure Function?::A function where given a set of inputs, the function returns the same output every time; deterministic

What is an interpreter?::A program that directly executes source code line by line, without converting it into machine code

What is ECMA script?::The official specifications that detail what JavaScript can and can't do

Every programming language needs what key thing in order to be able to execute?::A runtime environment

What is Node.js?::A runtime environment that allows JavaScript to be executed outside of the browser

What 2 things are required to create and run a program on a computer?
?
- Programming language
- Runtime Environment

What does a runtime environment include?
?
- A compiler or interpreter
- Extra facilities to help the programming language interact with its environment
	- APIs