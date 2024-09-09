#OOP/W1 
## General knowledge

- Python is **strongly** but **dynamically** typed language
	- **strongly** - this means variables have a type and the type matters when performing operations on the variable
	- **dynamically** - this means the type of variable is determined only during runtime

## Variables

- Variable defined inside a function is only "known" within that function (**variable scoping**)
- Python variables should follow **snakecase** 
	- ex. `my_great_variable`
- Constants should be uppercase
	- ex. `NUMBER_OF_ATTEMPTS = 2`
- All variables have a type: `type(my_variable)`

## Numeric types

```
round_number = 20  
float_number = 42.4  
string_number = "100"  

int(float_number) # 42  
int(string_number) # 100 (not '100' !)  
float(round_number) # 20.0
``` 
- Types: 
	- `int`,
	- `float`,
	- `complex`
- Integer division and modulo
	- `14 // 3 == 4`
		- also called **floor division** 
		- divides and rounds to the nearest whole number
	- `14 % 3 == 2`
		- divides and returns remainder
- Because of binary representation of floating point numbers, rounding errors can happen
- Complex math are done with `import math`
	- `math.sqrt`
	- `math.pow`
	- `math.log`

## Booleans

- Remember that `not (A and B)` is `not A or not B` , and is not the same as `not A and not B`
```
not_attractive = not (rich and beautiful)  
not_attractive = not rich or not beautiful  
very_unattractive = not rich and not beautiful
```
## If
```
if condition:  
# runs if condition is True  
elif another:  
# runs if condition is False and another is True  
else:  
# runs if condition is False and another is False
```
- one-liner version:
	```can_drink = True if age > 19 else False```

## Collections

- `list`, `tuple`, `set`, `dict`
- "contain" multiple elements
- Elements can be of different types

| Collection | Ordered (sortable) | Comments                                                           |
| ---------- | ------------------ | ------------------------------------------------------------------ |
| list       | yes                | Mutable                                                            |
| tuple      | yes                | Not mutable                                                        |
| set        | no                 | Mutable. Elements are "unique"                                     |
| dict       | no                 | Key-pair values (similar to hashmaps or arrays in other languages) |
### Lists and tuples
- A list is a collection of ordered elements (sequence)
	- Sequences in Python are ordered (you can sort them)
- Lists can be mutated
	- can change values of the element
- Tuples can **NOT** be mutated
- `sequence[index]`accesses element at `index` in `sequence`
- Uses `append` 
```
# Lists  
my_list = [4, 5, 6]  
another_list = list(1, 2, 3) # Another way to define a list  
my_list.append("something") # Add an element at the end of the list  
my_list[0] # Access an element by its position in the list  
(starts at 0)  
my_list[2] = "hello" # Change values  
new_list = my_list + another_list # Concatenate lists with +  
my_list.extend(another_list) # Similar to above, but modifies in place!  

# Tuples  
my_tuple = (1, 2, 3)  
another_tuple = tuple("hello", "world")  
my_tuple[1] # like lists  
my_tuple[0] = 0 # ERROR! Tuples are immutable
```

### Sets
```
my_set = set(1, 1, 1, 2, 3) # Elements are unique - the set contains {1, 2, 3}  
another_set = {"hello", "hello"}  
s[0] # ERROR! Sets are not ordered or indexed
```

#### Iterate on collections

- for `variable` in `collection`:
``` 
my_list = [1, 2, 3, 4]  
for value in my_list:  
	print("Value:", value)
```
- Do not iterate with indexes
```
# This is BAD - don't do it  
my_list = [1, 2, 3, 4]  
for idx in range(len(my_list)):  
	print("Value:", my_list[idx])
```
- `range(len(my_list))`creates a sequence of indices which is then used to access each element
	- why not iterate directly over each element of the list instead? 
- Less readable
- Error-prone
	- When you use `range(len(my_list))`, you rely on the list length to iterate, which increases the chance of off-by-one errors or index out-of-range errors if the list gets modified

#### Useful functions/properties
```
my_list = [1, 2, 3, 4, "hello"]  
len(my_list) # Number of elements in the list  
5 in my_list # False: 5 is not in the list  
"hello" in my_list # True
```

### Dictionaries

- Type is `dict`
- Very useful data type
	- maps **keys** to **values
- Are not ordered, can **NOT** sort 
- `dictionary[my_key]` access the element at key `my_key` in dictionary
- Has methods:
	- `keys()`
	- `values()`
	- `items()`
	- `update()`
```
my_dict = {"hello": "goodbye", 1234: "sunshine"}  
my_dict = dict((("hello", "goodbye"), (1234, "sunshine")))  
my_dict["hello"] # 'goodbye'  
my_dict["test"] = "something" # Add values to the dict  
my_dict[1234] = "rain"        # Keys are unique  
my_dict.keys()                # List of keys  
my_dict.values()              # List of values  
my_dict.items()               # List of key/value pairs
```

#### Iterate on dictionaries

```
for key, value in my_dict.items():  
	print("Key:", key, " - Value:", value)  
	
# Similar, by using keys  
for key in my_dict.keys():  
	print("Key:", key, " - Value:", my_dict[key])  
	
# Not using keys, looping on values only  
for value in my_dict.values():  
	print("Value:", value)
```

# Strings (text)

- Very much like a "list of characters"
- In Python, **strings are immutable**
- Type: `str`
	- `'text'`
	- `"text"`
	- `"""text"""`
- Useful methods:
	- `split()`
		- `"abc de f".split()` => `["abc", "de", "f"]`
	- `join()`
		- `" ".join(["abc", "de", "f"]) => "abc de f"`
	- `upper()`
	- `lower()`
	- `isnumeric()`
- Use f-strings:
	- `my_string = f"Hello {name}, nice to meet you!"`

```
my_string = "hello world"  
my_string[0] # 'h'  
my_string[0] = "H" # ERROR! Strings are immutable  
my_string.upper() # 'HELLO WORLD'  
my_string.split(' ') # ['hello', 'world']  
' '.join(['hello', 'world']) # 'hello world'  
'HELLO WORLD'.lower() # 'hello world'  
'world' in my_string # True
```

## Iterate on strings like lists

```
for letter in my_string:
	print(letter)
```

## Convert strings to numbers and vice-versa

```
my_string = "12345"  
int(my_string) # 12345  

another = "abc"  
int(another) # Raises an Exception!
```

# Functions

- Functions have **parameters** and receive **arguements**
- They return a value (of any type)
```
def register_student(student_id, name, international=False, scholarship=False):  
# Do something with the parameters  
return True
```
- The function `register_student` takes 4 parameters (or arguments)
	- `student_id` and `name` must be provided in this order
		- they are positional arguments
	- `international` and `scholarship` are _keyword_ arguments
		- they do not have to be provided because they have default values

- Keyword arguments can be provided in any order by using their names
```
register_student("A01209697", "Tim", scholarship=True, international=True)  
# This is a valid call, even if the keyword arguments are in a different order!
```

## Return values

- All functions return "something" using the `return` statement
- If `return` statement is omitted, function will return `None`
- A function returns **ONE** value - but the value can be a collection

# Exceptions

- Errors in code **raise** exceptions
- You can manually and voluntarily raise an exception
- You can catch exceptions by using `try ... except`

```
def say_hello(name):  
	if name == "Tim":  
		raise RuntimeError("This name is not allowed.")  
	return f"Hello {name}."
```

```
try:  
	text = say_hello("Tim")  
	print(text)  
except RuntimeError:  
	print("The name you provided is not allowed")
```

- Avoid using empty `try / except` statements (without specifying the exception)
	- harder to debug
	- bad practice

# Files and paths

```
with open("my_file.txt", "r") as fp:
	data = fp.read()
```
- Always use `with`
	- opens and closes file for you 
- 99% of the time you should use **relative paths**
- File extensions do not matter:
	- `whatever.docx` saved from Word is actually a ZIP file
- File formats are a convenience, a file is a file
- It is common to distinguish:
	- **Text files** (contains data that can be printed/read on screen)
	- **Binary** (contains data that are not characters)

# Python modules and `import`

- Use `import` to import another piece of code in your program
```
import math

math.sqrt(3)
```

```
from math imoprt sqrt

sqrt(3)
```

- Imports will lookup modules in the following order:
	1. in the standard library
	2. (usually) in the current folder
	3. see `sys.path` for a list of folders

- Typical built-in modules to know:
	- `os`
	- `sys`
	- `math`
	- `random`
	- `csv`
	- `pathlib`
	- `json`

# Debug your programs

- Use the debugger
- Use `print`, it's better than nothing
- Read the error messages
- Every time you make a change, **run the code**
- Don't make multiple changes to code
	- Fix one problem at a time

# Docstrings and documentation/comments

- In functions and files, write docstrings to inform users about what your code does
	- `"""text ... """`
- Add inline comments to explain complicated steps in your program
```
def my_func(a, b):  
	"""Takes two arguments and returns their average (sum / 2)"""  
	output = float(a) + float(b) # We force conversion to float  
	return output / 2
```

# Code structure

- Separate code into functions
- Separate functions into modules (Python files)
- Organize modules into packages (files in folders)
	- Don't forget `__init__.py` for packages
- Use `if __name__ == "__main__":`
	- To debug and prevent unwanted code execution
- Create a single entry point in your program and use modules/packages to organize the logic
```
├── component_1  
│ ├── __init__.py  
│ └── sub_package  
│ ├── __init__.py  
│ ├── sub_module_1.py  
│ └── sub_module_2.py  
├── component_2  
│ ├── __init__.py  
│ └── [... files ...]  
├── component_3  
│ ├── __init__.py  
│ └── [... files ...]  
└── main.py
```

# Don't do these

- Use `try ... except` without specifying exception you want to catch
- Use absolute paths

-  Use mutable default arguments for function parameters (like [] or {})
```
def append_to_list(value, my_list=[]):
    my_list.append(value)
    return my_list

# Calling the function multiple times
print(append_to_list(1))  # Output: [1]
print(append_to_list(2))  # Output: [1, 2] (Unexpected!)
print(append_to_list(3))  # Output: [1, 2, 3] (Even more unexpected!)
```
- This is an issue because when you define `my_list=[]`, Python created a default list once and reuses it every time the function is called, rather than creating a new list every call
	- Avoid this issue by defining `my_list=None` instead and initializing the argument inside the function
		- this ensures a new list is created every time the function is called
```
def append_to_list(value, my_list=None):
    if my_list is None:
        my_list = []  # Create a new list for each function call
    my_list.append(value)
    return my_list

# Now each call works as expected
print(append_to_list(1))  # Output: [1]
print(append_to_list(2))  # Output: [2]
print(append_to_list(3))  # Output: [3]
```

- Modify a list while iterating over it
	- use a list comprehension
		- creates a new list based on conditions
	- or copy the list first:
		- `my_copy = my_list.copy()`
		- `my_copy = my_list[:]`
		- `my_copy = my_list` **does not copy the list**


# [[2515 Week 1]]


# Flash Cards

What is a strongly typed language?::Variables have a type and the type matters when performing operations on the variable

What is a dynamically typed language::means the type of variable is determined only during runtime

```
something = "This is something"

def example_function():
	something = " "
	return something

example_function()
print(something)
```
What is the output of this code snippet?
?
"This is something"
- Variables defined within a function are only known within that function

Python variables should follow what naming convention?
?
snakecase
ex. 
- `my_great_variable`

How do you indicate a variable is a constant in Python?
?
Variable should be in uppercase
ex. 
- `NUMBER_OF_ATTEMPTS = 2`

What type of division is this?
`14 // 3 == 4`
?
Floor division or Integer division
- Divides and rounds to the nearest whole number

```
rich = True
beautiful = True

attractive = rich and beautiful
not_attractive = not (rich and beautiful)
not_attractive_2 = not rich or not beautiful
very_unattractive = not rich and not beautiful
```
What boolean values are:
`attractive`,
`not_attractive`, 
`not_attractive`, 
and `very_unattractive`?
?
attractive = True
not_attractive = False
not_attractive_2 = False
very_unattractive = False
**Remember that "`not (A and B)`" is "`not A or not B`", and is not the same as "`not A and not B`"**

What is the key difference between a `list` and a `tuple`?::A `list` is mutable (can be changed), while a tuple is immutable (can't be changed after creation)

True or False?
Sets can contain duplicate elements
?
False

What methods are used to insert elements to a:
`list`,
`tuple`,
`set`,
`dict`
?
`list`= append()
`tuple`= no method; immutable
`set`= add()
`dict`= update()

You should avoid iterating with?
?
Indexes
```
# This is BAD - don't do it  
my_list = [1, 2, 3, 4]  
for idx in range(len(my_list)):  
	print("Value:", my_list[idx])
```

True or False? 
You can define a set in Python like so:
`my_set = {1, 2, 1, 1, 3}`
?
True

True or False?
Dictionaries can be sorted
?
False
- Dictionaries are not ordered, therefore they can't be sorted

What method should you use to iterate through both key and value of a Python dictionary?
?
`.items()`
```
for key, value in my_dict.items():
	print("Key:" + key + " - Value:" + value)
```

What method should you use to iterate though the keys of a Python dictionary?
?
`.keys()`
```
for key in my_dict.keys():  
	print("Key:" + key + " - Value:" + my_dict[key])
```

Are strings mutable (can be changed) or immutable (can't be changed)?::Immutable

## CONTINUE FROM STRINGS