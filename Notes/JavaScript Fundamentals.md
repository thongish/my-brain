#WEB/W1 \
# What is an expression?

- A sequence of **operators** and their **operands**
- Evaluating an expression produces a **result value**
	- Evaluating expressions may generate a **side effect**
		- i.e. evaluating `{js} console.log("BCIT is doodoo")`has a side effect of printing a line of characters in the console

# Data types

- JavaScript programs manipulate data, and each value has a type
- ECMAScript standard defines a few basic data types:
	1. Boolean
	2. Number
	3. String
	4. null and undefined
	5. objects
## Number

- JavaScript uses 64 bits to store numbers
- There are also special numbers in JavaScript:
	- `{js}10 / 0;` = infinity
	- `{js}-10 / -;`= -infinity
	- `{js}0 / 0; `= NaN

# Variables and assignment

- Each variable needs a name, called an **identifier**
- **Identifiers** are the names for values and things in JavaScript
	- Identifier must start with a letter, underscore `{js}_`, or dollar sign `{js}$`; subsequent characters can also be digits `{js}0 to 9`
	- There are 35 keywords in JavaScript that can't be used as identifiers
		- [List of keywords](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Lexical_grammar)
- Camel Case example: `{js}thisIsCamelCase`

## How do we name things?

- Use intention-revealing names (why, what, and/or how)  
- Avoid disinformation (no false clues)  
- Make meaningful distinctions (no noise words)  
- Use pronounceable names  
- Use searchable names (no single letter identifiers)  
- Pick one word per concept, i.e., don’t use `{js}sum` and `{js}total` and `{js}aggregate` in the same program
# Operators and operands

## Increment and decrement

- Two ways to add/subtract from a number
	- Postfix
		- `{js}a++` or `{js}a--`
		- Add/subtract 1 to or from `{js}a` and return the old value of `{js}a` while overwriting the original value
	- Prefix
		- `{js}++a` or `{js}--a`
		- Add/subtract 1 to or from `{js}a` and return the new value

# Resources

- [AirBNB Style Guide](https://github.com/airbnb/javascript)
- [Modern JavaScript Tutorial](https://javascript.info/)
	- If use this site, ignore:
		- 2.3,
		- 2.6,
		- 2.12
		- 2.17
		- 2.18

# Flash cards


What is an expression?::A sequence of operators and their operands that, when evaluated, produces a result value and may generate a side effect.
<!--SR:!2024-09-29,1,210-->

What is a side effect in the context of evaluating an expression?::An unintended change or output resulting from the evaluation of an expression, such as printing a line of characters to the console.
<!--SR:!2024-09-29,1,210-->

What are the basic data types defined by the ECMAScript standard?
?
- Boolean, 
- Number, 
- String, 
- null and undefined, 
- objects.
<!--SR:!2024-09-29,1,210-->

How does JavaScript store numbers?::JavaScript uses 64 bits to store numbers.
<!--SR:!2024-09-29,1,210-->

What are some special numbers in JavaScript?
?
- Infinity (`{js}10 / 0`), 
- -Infinity (`{js}-10 / -0`), 
- and NaN (`{js}0 / 0`).
<!--SR:!2024-10-06,8,250-->

What is a variable in JavaScript?::A storage location identified by a name (identifier) used to hold data values.
<!--SR:!2024-10-25,15,230-->

What is an identifier in JavaScript?::The name given to a variable or other value in JavaScript, which must start with a letter, underscore (`{js}_`), or dollar sign (`{js}$`), with subsequent characters allowed to be digits (`{js}0 to 9`).
<!--SR:!2024-09-29,1,210-->

What are some rules for naming identifiers in JavaScript?
?
- Use intention-revealing names, 
- avoid disinformation, 
- make meaningful distinctions, 
- use pronounceable and searchable names, 
- and pick one word per concept.
<!--SR:!2024-09-29,1,210-->

What is camel case in naming conventions?::A naming convention where the first word is lowercase and each subsequent word starts with an uppercase letter, e.g., `{js}thisIsCamelCase`.
<!--SR:!2024-10-06,8,250-->

What are the two ways to increment or decrement a number in JavaScript? and what do they return?::Postfix (`{js}a++` or `{js}a--`) which returns the old value, and Prefix (`{js}++a` or `{js}--a`) which returns the new value.
<!--SR:!2024-09-29,1,210-->