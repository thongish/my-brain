## General knowledge

- Python is **strongly** but **dynamically** typed language
	- **strongly** - this means variables have a type and the type matters when performing operations on the variable
	- **dynamically** - this means the type of variable is determined only during runtime
## Variables

- Variable defined inside a function is only "known" within that function (**variable scoping**)
- Python variables should follow **snakecase** 
	- ex. ` my_great_variable`
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
- Uses `.append` 
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
	- `.split()`
		- `"abc de f".split()` => `["abc", "de", "f"]`
	- `.join()`
		- `" ".join(["abc", "de", "f"]) => "abc de f"`
	- `.upper()`
	- `.lower()`
	- `.isnumeric()`
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
---
# Why venvs are useful

- Allows separation of  dependencies between projects
	- Useful if projects require different versions of libraries or packages
- Isolate global environment
	- Installing packages globally can affect all of your python projects
	- Can lead to compatibility issues
- Makes reproducing program environment easier
# Best practices

- Use `venv` module from Python
- Created one venv per project/assignment
	- Create using `py -m venv venv`
		- This uses the module `venv` and creates folder called `venv`
		- `py -m venv folder`
- The venv will be created in a folder
	- Will contain binaries (scripts)
	- Will contain libraries required by the program to run
	- Folder typically called `venv`
- The venv must be **activated** in order to work
	- Activate using `activate` script in `venv/Scripts`
- Once venv is active, the **only** commands needed are `` and `pip`
- Don't use `py`, `3`, etc.
---
# Important concepts

- Python code is written in files
- Each file is a Python module

```
# Contents of my_print.py

MY_MESSAGE = "Hello!"

def my_print_func(text):
	print(MY_MESSAGE)
	print(text)
```
- You can import other files,
```
# Contents of main.py
import my_print

def main():
	my_print.my_print_func("Example.")
	print(my_print.MY_MESSAGE)
```
-  The entire `my_print` module is imported
- You can access functions or variables using `.` notation
	- Can also access "properties" with `.` notation
- Everything in Python is an object
- When module is imported, the code it contains is **executed**
- Make sure to use `if __name__ == "__main__":` to prevent side effects

- or specific symbols of a module:
```
from my_print import MY_MESSAGE  

print(MY_MESSAGE)
```
# Python packages

- Packages are collections of modules
- Several files in a folder
- Is a folder with `__init__.py` file in it
	- can work without one, but should always have one
## About packages

- Python packages can contain modules, and other packages
```
├── constants.py
├── display       # This is the PACKAGE display
│ ├── __init__.py
│ └── show_map.py # It contains the MODULE show_map
├── logic         # This is the PACKAGE logic
│ ├── __init__.py
│ ├── computer    # It contains a PACKAGE computer
│ │ ├── __init__.py
│ │ └── aimbot.py # Which contains a MODULE aimbot
│ │               # This module has a FUNCTION shoot() in its code
│ ├── game.py     # This module belongs to the PACKAGE computer
│ └── win.py
└── main.py
```
# Importing modules and packages

- You can import the whole package just like modules: `import logic`
	- and then use `.` to access submodules/packages
```
import logic  

logic.computer.aimbot.shoot() 
# In the PACKAGE logic
# Look for the PACKAGE computer  
# And find the MODULE aimbot  
# Run the FUNCTION shoot

logic.game.start()  
# In the PACKAGE logic  
# Look for the MODULE game  
# Run the FUNCTION start
```
## Importing sub-packages

```
import logic.game  

logic.game.start() # OK  

logic.computer.aimbot.shoot() # DOES NOT WORK (we only have logic.game)
```
## Importing and renaming

- Can be convenient for long/complicated names
```
import logic.computer.aimbot as bot

bot.shoot()
```
## Using `__init__.py` to allow easier access to subpackages

- When Python encounters an `import` statement and the symbol imported is a package, the `__init__.py` file will automatically run
- This file can import functions/variables from submodules and packages to allow for easier imports
```
├── logic  
│ ├── __init__.py  
│ ├── constants  
│ │ ├── __init__.py  
│ │ ├── player.py       # Contains NUMBER_PLAYERS = 10  
│ │ └── bot.py          # Contains AIMBOT_PRECISION = 1.0  
│ └── game.py  
└── main.py
```
### `logic/__init__.py`
```
from .constants.player import NUMBER_PLAYERS  
from .constants.bot import AIMBOT_PRECISION
```
### `main.py`
```
from logic import NUMBER_PLAYERS  

# Or even  
from logic import NUMBER_PLAYERS, AIMBOT_PRECISION
```
## Packages and paths

- When running a Python program, the working directory is the **directory where you ran the Python command**
- This can have an effect when testing/developing programs
```
├── my_package  
│ ├── __init__.py  
│ └── my_module.py  
├── file.txt  
└── main.py
```

```
# Contents of my_package/my_module.py  
open("file.txt", "r")
```
- ` my_package/my_module.py`: WORKS
- ` -m my_package.my_module`: WORKS (preferred way)
- `cd my_package`, and then ` my_module.py`: DOES NOT WORK (there is no "main.txt" file in the `my_package` folder)

---
# Why test?

- The only way to make sure "everything works"
- Automated tests are easier and quicker to run
- One button approach
	- Run a command, and you know whether or not the code works
- Unit tests are automated tests
	- Operate at the lowest level possible
		- only validate basic elements of a program
	- Do not validate how objects interact with each other (this is **integration testing**)
# Unit tests

- Are fast to run (few seconds max)
- Are easy to write (when written at the same time as the actual code)
	- This is called **Test Driven Development** (TDD)
- Can be automated and scheduled
	- Every night
	- Upon each commit in a git repository (**continuous integration**)
- Makes sure sure that the requirements for the programs are respected by the developer; the program does what it is supposed to do
# Run tests with `pytest`

- At the root of the project, run `pytest`
	- `pytest` will scan and discover all tests in the test files
	- Test files are any files that match the patterns:
		- `test_*.py`
		- `*_test.py`
	- Tests are functions/methods whose names start with `test_`
	- Tests can be:
		- regular functions outside of classes
		- methods inside classes, whose names start with `Test`
- Very often, tests are located in the `tests` folder, at the root of the folder
## Examples

```
# test_something.py  
def test_thingy():         # This is run by pytest  
	pass  
def thing():               # But not this  
	pass  
class Something:  
	def test_thing(self):  # Also not this!  
		pass  
class TestSomething:  
	def test_thing2(self): # This is run by pytest  
		pass
```
# How to write a test

## Code to be tested
```
def add_values(a, b):
	return a+b
```
## The test
```
def test_add_values():
	result = add_values(2,3)
	assert result == 5     # This line makes sure the output is the one we expect
```
## How to test for exceptions?

- Sometimes *expected* that your code raises exceptions
```
def add_values(a, b):  
	if type(a) is not int or type(b) is not int:  
		raise TypeError("Invalid value")  
	return a+b
```
### The test
- Use the `with pytest.raises(<NAME>)` to catch the expected Exception `<NAME>`
```
import pytest  

def test_add_values_invalid():  
	with pytest.raises(TypeError):  
		result = add_values([1], [2])
```
# Code coverage and unit testing

- Goal of unit testing is to make sure every aspect of the code is tested and working
- Can measure "how much code" is covered by unit tests; the **code coverage**
- Typical for teams to aim for at least 80% code coverage, and sometimes even 90%
- [5 questions every unit test must answer](https://medium.com/javascript-scene/what-every-unit-test-needs-f6cd34d9836d)
## Code coverage in Python

- Use the `coverage` library (an external dependency), together with `pytest`
- Install in venv with `pip install pytest-cov`
- Can then run tests and add coverage with the `--cov` options
	- can be a Python module
		- `pytest --cov=add`
	- or a Python package
		- `pytest --cov=.` (use `.` for the current folder)
- `coverage` will report about all the Python files used to run your program
## Coverage reports

- Generate nice looking HTML report
	- `pytest --cov=. --cov-report=html`
		- This will create/update contents in the `htmlcov` folder 
# Developing with a test-oriented mindset
## Goals

- Make sure tests are actually written
- Validate the requirements and design
- You become the "user" of the code you are about to write
- You can work with stakeholders to resolve the anomalies/gaps
## Issues

- Requires discipline
- "I am a developer, I want to code and not test"
- May appear useless at first sight
# Unit testing best practices

- Be reasonable
- No more test code than application code
- Code coverage of 80% is a good objective
- One minor change in the tests = one minor change in the application
- True for software development in general
---
# Definitions OOP

- **Class**
	- Defines a general category (i.e. book, bank account)
	- Blueprint (or template) for creating an object
	- A custom data type
- **Object** or **Instance**
	- A "thing" created out of a class
- **Attributes**
	- Values for a specific object
- **State**
	- The current values of the attributes in an object

- A book is a **class** = the abstract concept of something you can read
- "Harry Potter" that you bought at the library 10 years ago is an instance of a book
	- It is one specific, concrete book object that follows all the "laws of books"
# Important concepts

## Modelization

- The objective of a model is to "describe" an object
- How can we describe a person?
	- For the government: name, address, SIN \#
	- At BCIT: name, student number, program
	- At the hairdresser: first name, phone number, appointment date
- We represent the objects by creating a **model** and implement it using a class
## Encapsulation (and visibility)

- The state of an object should only be changed by the object itself
- Use behaviours (methods) to alter the state, instead of changing the attributes
- Some OOP languages have a visibility feature, where you can make attributes private
	- Python does not have it, but you can use `_` in the beginning of the attribute to mean it is private
- Using private attributes and using methods to change the state is called **encapsulation**
# Abstraction

- The implementation of behaviours of the object is the responsibility of the class
- Other objects should not depend upon private attributes or methods
- They should only use the public interface of the class (the public methods and attributes)
- Process of hiding the internal details of an application from the outer world
	- ex. I know how to call and use the string method `string.upper()` but I don't know the inner working of why and how it does what it does
# Class syntax in Python

- `class MyClassName:` to define a new class "block"
- Except for class variables, a class definition only has **methods**
- Methods are defined inside the class block, and receive `self` as first parameter
- A special method is `__init__`, always called upon initialization of the instance

```
class Student:  
	def __init__(self, name, student_number):  
		self.name = name  
		self.student_number = student_number  
		self.program = "CIT"  
	def display(self):  
		print(f"{self.name}, {self.student_number} - {self.program})  
		
john = Student("John Doe", "A01234567")  
john.display()  
bob = Student("Bobby", "A4432890")  
bob.display()
```
# The `self` parameter

- All functions within a class are called "methods"
- They receive an implicit parameter: `self`, which represents the current **instance**
- This allows **encapsulation**
	- i.e. each instance has its own version of the class attributes, and they are accessed with `self`
- **NEVER** use `self` outside of the class block
# Parameter validation

- Imagine the `student` class should not allow students with "invalid names"
- We will make it raise an exception if that is not the case

```
class Student:  
	def __init__(self, name, student_number):  
		if not name or type(name) is not str:  
			raise AttributeError("Name cannot be empty!")  
		self.name = name  
		self.student_number = student_number  
		self.program_name = "CIT"  
	
john = Student("", "A01234567") # Will raise an Exception!  
john = Student(42, "A01234567") # Will raise an Exception!
```
# Using Python `property`

- Python has a decorator which makes encapsulation and abstraction easier
- You can use the `@property` decorator on a method, and then it will behave as an **attribute**
	- This allows you to implement getters very easily
```
class Student:  
	[...]  
	@property  
	def info(self):  
		return f"{self.name} ({self.student_number})"  
		
john = Student("John Doe", "A01234567")  
# Note how we use info as if it were a variable!  
# We don't use () even though info is a method.  
print(john.info)
```
# Python properties: the setter

```
class Student:  
	[...]  
	@property  
	def program(self):  
		return self.program_name  
		
	@program.setter  
	def program(self, value):  
		if value not in ("CIT", "CST", "BTech"):  
			raise ValueError("Invalid program name!")  
		self.program_name = value  
		
john = Student("John Doe", "A01234567")  
print(john.program) # Runs the getter method (@property)  
john.program = "Btech" # Runs the setter method (@property.setter)  
john.program = "something" # Raises an Exception! (in @property.setter)
```

- You can only create a setter when you have a getter defined (property)
- The getter and setter methods are called the same name
	- You also need to use this name in the `@[name].setter` decorator
# Static methods and class methods

- You can define methods that are common to all objects of the same class
- Static methods do not get any reference tot he class or object
- Class methods receive a reference to the **class** when called directly from the class name
- This reference is typically called `cls`
- Use the `@staticmethod` decorator for static methods (no reference)
- Use the `@classmethod` decorator for class methods (reference to class)
## Static method example

```
class Student:  
	[...]  
	@staticmethod  
	def check_program(value):  
		# This is a static method. It does not receive an implicit argument.  
		# It does not have access or know about the class / instance  
		return value in ("CIT", "CST", "BTech")  
		
Student.check_program("CIT") # will return True  
john = Student("John Doe", "A01234567")  
john.check_program("CIT") # will also return True
```
## Class method example

```
class Student:  
	PROGRAMS = ("CIT", "CST", "BTech")  
	[...]  
	@staticmethod  
	def check_program(cls, value):  
		# This is a static method. It does not receive an implicit argument.  
		# It does not have access or know about the class / instance  
		return value in cls.PROGRAMS  
		
Student.check_program("CIT") # will return True  
john = Student("John Doe", "A01234567")  
john.check_program("CIT") # will also return True
```
# Class variables

- Class variables are attributes that are common to all objects of the same class
- They are defined in class block, but outside any methods
- The previous example uses a class variable `PROGRAMS`
- Class methods have access to class variable (but no instance variables)
- Static methods do not have access to class variables, nor instance variables
# What you REALLY need to know

- How to define a class: `class MyClass:`
- Understand what the constructor does ( `__init__` )  
- Understand what `self` is  
- Be able to write any instance methods  
- Because you define an instance variable `self.something` in`__init__` ...  
	- DOES NOT MEAN that `__init__` will take it as a parameter!  
- Understand what inheritance, but also understand when NOT to use it (i.e. most of the time by yourself, unless you are using a library / package)  
- In the context of this course, using class variables and class / static methods and variables is a bad idea and  almost never happens, except when working with SQLAlchemy. If you are using them, make sure you know what  you are doing.  
- There is very little to learn or know about Object Oriented Programming. It is mostly about how you "view the  world" in your program.
---
# Classes and class diagrams

- Classes and objects have:
	- Attributes
	- Behaviours
- We can easily represent classes using a diagram, called a **class diagram**
- UML is just a common language:
	- standards vary by team/project
# Required items in a class diagram

- The class diagram shows:
	- Name of the class
	- Attributes and their types
	- Methods, with:
		- the parameters and their types
		- the return value and its type

![[Pasted image 20241007124823.png]]
## Comments

- The `@property` decorator can be confusing:
	- it "looks like" an attribute, but works through methods
	- It is generally located in the methods section of the class diagram
	- In above diagram,
		- `mileage` and `mileage()` one is a `@property` decorator and the other is a `@property.setter`
- The convention in Python is to use `_name` for a private variable called `name`
- In UML, you use a `-` for private attributes, and `+` for public attributes
# Relations in UML diagrams

- Simply represented by a line connecting the two classes
- Sometimes the **nature** of the relationship is expressed in the diagram
- Different types of relationships:
	- Composition
	- Aggregation
	- Extension (or inheritance)
- Each type of relationship has a different "line" representation
# Aggregation vs composition

- Aggregation is when two objects are related, but can "exist" independently of each other
- Composition is when one object cannot exist without the other
- 
- A car "system" is made of a car and a driver
- A car is made of an engine and a body
	- If the car is destroyed, the driver still exists
	- If the car is destroyed, the engine does not exist anymore

![[Pasted image 20241007125821.png]]

---
# Object relationships

You create an aggregation/composition relationship by keeping a "reference" from one object to another
# Composition

- Example: a hand **has** 5 fingers
- We choose to use a composition relationship
```
class Finger:  
	def flick(self):  
		print("Oh no.")  
		
class Hand:  
	def __init__(self):  
		self._fingers = [Finger() for _ in range(5)]  
		
	def thumbs_up(self):  
		self._fingers[0].flick()
```
- The `Finger` objects are created by the `Hand` objects (when the `Hand` disappears, so do the fingers)
- The `Hand` can keep track and interact with the `Finger` objects through the private variable `self._fingers`:`self._fingers[2].flick()
# Aggregation

- Example: the car and the driver
```
class Driver:  
	def __init__(self, name):  
		self.name = name  
		
class Car:  
	def __init__(self, driver):  
		self._driver = driver
```
- You can associated the objects when creating the car:
```
tim = Driver("Tim")
my_car = Car(Tim)
my_car = Car(driver=tim) # also works
```
# Composition and Aggregation

- In general, in a composition relationship, composite objects are created when the main object is created (in the `__init__` method)
	- Can also happen elsewhere (`def add_finger(self)`)
- In aggregation relationships there are usually methods in the public interface that allow you to associate/disassociate objects
	- Can be sometimes related to setters
```
class EvoCar:  
	def __init__(self):  
		self._driver = None  
		
	def start_rental(self, new_driver):  
		self._driver = new_driver  
		
	def end_rental(self):  
		self._driver.charge_rental()  
		self._driver = None  
		
tim = Driver("Tim")  
prius = EvoCar()  
prius.start_rental(tim)  
prius.end_rental()
```
# Inheritance

- Used when several objects are part of the same family:
	- they share similar attributes
	- they share similar behaviours

```
class Vehicle:  
	def drive(self):  
		pass  
		
	def stop(self, distance):  
		self._mileage += distance  
		
class Car(Vehicle):  
	""" Car will automatically INHERIT from all attributes and methods of       Vehicle """  
	pass  
	
class SUV(Vehicle):  
	""" SUV will automatically INHERIT from all attributes and methods of       Vehicle  
	But you can add attributes / methods too """  
	is_awd = True
```

- All attributes and methods of the parent class are **inherited** by the child class
- If attribute is defined in both the parent and child class, the **child class** has precedence
- You can travel up the inheritance tree by using `super()`
	- `super()` will give access to the parent class (and its methods/attributes)

```
class Car:  
	def __init__(self, model, brand, mileage=0):  
		self.brand = brand  
		self.model = model  
		self.mileage = mileage  
		
class Chevrolet:  
	def __init__(self, model, mileage=0):  
		super().__init__(model, "Chevrolet", mileage)
```
## Inheritance limitations

- Inheritance is great but should be used sparingly
- It can be complicated to understand which method or variable comes from which class
- There are a lot of occurrences where inheritance can be replaced with composition
- Inheritance can be really useful when used to create "better versions" of standard Python types

```
class Grades(list): # Grades derives from builtin `list`  
	@property 
	def average(self):  
		return sum(self)/len(self)
		  
grades = Grades([83, 90, 74, 23])  
print(grades.average) # 67.5
```

**Combine them with other objects**
```
class Student:  
	def __init__(self, grades):  
		self._grades = Grades(grades) 
		 
	@property  
	def does_pass(self):  
		return self._grades.average > 50  
		
tim = Student(grades=[83, 90, 74, 23])  
print(tim.does_pass) # True
```
## Using inheritance to create abstract classes

- You can use inheritance to define "generic classes" that only define a specific public interface, **without implementing it**
- The child class will inherit all attributes from the parent class, and will override the public interface methods

```
class Animal:  
	def __init__(self, name):  
		self._name = name  
		
	def sound(self):  
		raise NotImplementedError("Abstract method for animal sound must be implemented by the child class")
		  
	def show_name(self):  
		print(self._name)
		  
class Cow(Animal):  
	def sound(self):  
		return "MOO"  
		
class Dog(Animal):  
	def sound(self):  
		return "WOOF"
```
## From inheritance to polymorphism

```
daisy = Cow("Daisy")  
daisy.sound() # MOO!  
daisy.show_name() # prints "Daisy"  
isinstance(daisy, Animal) # TRUE!  
isinstance(daisy, Cow) # TRUE!  

snoop = Dog("Snoopy")  
snoop.sound() # WOOF!  
snoop.show_name()  

for animal in (daisy, snoop):  
	animal.sound() # POLYMORPHISM!
```
- `animal` can be a cow or a dog, but it has an interface that defines `sound()`
- from the Python interpreter perspective, `animal` is just an object that happens to have a matching method available
- Note that `isinstance(daisy, Animal)` returns `True` even though daisy is a cow
	- Because `Cow` is a child class of `Animal`
	- A cow is also an animal
# Defining abstract methods in Python with `@abstractmethod` and `ABC`

```
from abc import abstractmethod, ABC  

class Animal(ABC):  
	def __init__(self, name):  
		self._name = name  
		
	@abstractmethod  
	def sound(self):  
		pass  
		
	def show_name(self):  
		print(self._name)
```

---
# Python built-in methods

- Everything in Python is an object
	- The base type (class) in Python is `object`
- Python defines several built-in methods
	- enclosed by `__`: the "**dunder**" - double underscore
- `__init__` is the constructor (initializes values)
- There are other ones:
	- `__new__` - the actual "constructor", outside the scope of this course
	- `__str__` - returns a string representation of the object
- Dunder methods are **magic** because they are run without being called explicitly
## Example: the `Person` class

```
class Person:  
	def __init__(self, name):  
		self._name = name  
		
	def __str__(self):  
		return f"Person: {self._name}"
```

- `__str__` will be called when casting the object into a string 
	- For example, in a `print` statement, or when using `str(my_instance)`
```
tim = Person("Tim")

print(tim)
# Also possible: str(tim)
```
# Other useful methods to override

- `instance` is an instance of the class considered

| Method                      | Goal                                                |
| --------------------------- | --------------------------------------------------- |
| `__str__(self)`             | For `print(instance)` or `str(instance)`            |
| `__len__(self)`             | Allows `len(instance)`                              |
| `__getitem__(self,key)`     | Allows `instance[value]` (can be a slice)           |
| `__call__(self)`            | Allows to use `instance()`                          |
| `__contains__(self, other)` | Allows to test `something in instance` expression   |
| `__iter__(self)`            | Allows to use `instance` as an iterator             |
| `__next__(self)`            | Returns the next value in the iteration (see above) |
# Dunder "mathematical" methods

| Method    | Goal                          |
| --------- | ----------------------------- |
| `__add__` | Using `instance + something`  |
| `__sub__` | Using `instance - something`  |
| `__mul__` | Using `instance * something`  |
| `__pow__` | Using `instance ** something` |
| `__mod__` | Using `instance % something`  |
| `__eq__`  | Using `instance == something` |
| `__lt__`  | Using `instance < something`  |
| `__le__`  | Using `instance <= something` |
| `__gt__`  | Using `instance > something`  |
# Implementing the `__lt__` method for the Score class

```
class Score:  
	def __init__(self, name, score):  
		self.name = name  
		self.score = score  

	def __lt__(self, other):  
		if type(other) is not type(self):  
		# Makes sure comparison only between score objects and nothing else
			raise TypeError("Unsupported type")  
		# We compare the score attribute  
		return self.score < other.score
```

- Sort list of scores:
```
scores = [Score("Tim", 0), Score("John", 1000), Score("Sarah", 2000)]  
print(sorted(scores)) # Will display the sorted result  
scores.sort()         # Will sort in place
```
# Design pattern: using collections

The high scores board is a **collection** of scores
```
class HighScores:  
	def __init__(self):  
		self._scores = list()  
	# We would need to manage scores here, or use aggregation  
	def __len__(self):  
		return len(self._scores)
```

And then:
```
hiscores = HighScores()
hiscores.add(tim_score)
len(hiscores) # will return 1 (1 score in the list)
```
# Using `operator` for sorting (and other things)

- Python standard library comes with the `operator` module
- Provides premade functions to access:
	- items
	- elements of an object
	- collection
- `itemgetter` - to get items from lists/dictionaries by key (index for a list or key for a dictionary)
- `attrgetter` - to get attributes from objects (by attribute name)

**With lists**
```
menu = [  
	("Pizza", 10),  
	("Pizza slice", 3),  
	("Fountain drink", 2),  
	("Cookie", 4),  
]  
# Each element in the menu is a tuple (~list)  
# We want to sort on the item with index 1  
sorted(menu, key=operator.itemgetter(1))
```

**With dictionaries**
```
menu = [  
	{ "name": "pizza", "price": 10, "in stock": 10 },  
	{ "name": "drink", "price": 2, "in stock": 50 },  
	{ "name": "cookie", "price": 4, "in stock": 20 },  
	{ "name": "pizza slice", "price": 3, "in stock": 15 },  
]  
sorted(menu, key=operator.itemgetter('price'))
```

**With objects**
```
hiscores = [  
	Score(name="Tim", score=20),  
	Score(name="John", score=0),  
	Score(name="Sarah", score=100),  
]  
# Sorting on the name attribute  
sorted(hiscores, key=operator.attrgetter('name'))
```
# Collections: getting elements with `__getitem__`

```
class HighScores:  
	def __init__(self):  
		# This is a list of scores  
		self._scores = list()  
		
	def __len__(self):  
		return len(self._scores)  
		
	def __getitem__(self, idx):  
		return self._scores[idx]  
		
hiscores = HighScores()  
# Add scores to the instance, and then:  
print(hiscores[0].scores) # First score in the list  
print(hiscores[-1].scores) # Last score in the list
```

---
# Fixtures

- In tests, it's common to create an object and run all the different methods and check their behaviours
- Each test function will test a specific feature of the class
- You may end up creating the same object over and over in all of your test functions
- **Fixtures** are meant to solve this problem by defining objects that can be reused in different test functions
# Pytest fixtures

```
import pytest

@pytest.fixture
def bank():
	bank = Bank("BCIT Bank")
	return bank

def test_bank(bank):
	assert bank.name == "BCIT Bank"
```

- Defined using the decorator `@pytest.fixture`
- They are regular functions
- The value returned is the "fixture" that you can use in your test function
- To make a test function use a fixture, use its name as an argument in a test function

```
import pytest  
	@pytest.fixture  
	def tim():  
		return Customer("Tim", "A0001")  
		
	@pytest.fixture  
	def checking(tim):  
		return CheckingAccount(tim)
```
- You can next fixtures
# Mocks and patching

**The problem we are trying to solve:**
```
class BankAccount:  
	[...]  
	@property  
	def balance(self):  
	""" Return the balance of the account """  
	[...]  
	
class BankCustomer:  
	def __init__(self):  
		self._accounts = list() 
		 
	def add_account(self): [...]  
	def total_balance(self):  
		return sum([account.balance for account in self._accounts])
```
- How do you test `BankCustomer` without testing `BankAccount` at the same time?
## Unit tests

- Unit tests should only test a specific class or function, and not the **dependencies** of that code
- There are some elements that you do not need to isolate,
	- whether `super()` works,
	- or if `list` is really a list
## Example: broken property in `BankAccount`

```
def test_bank_customer_total_balance():  
	tim = BankCustomer("Tim")  
	
	account = BankAccount("Test", 1000)  
	tim.add_account(account)  
	
	assert tim.total_balance == 1000
```
- Let's imagine there is a bug in the `balance` property of the `BankAccount` class
- This test will fail, because of the bug in **another class**
- We need to remove the dependency between `BankCustomer` and `BankAccount`
## Monkeypatching

- The `monkeypatch` fixture is available by default in Pytest
- You can use it in test functions to change the behaviour of certain objects or classes
- Very similar to `setattr` in Python
- In our case, we want to **monkeypatch** the `balance` attribute for the BankAccount class
- We are going to monkey patch it with a standard integer:

```
def test_bank_customer_total_balance(monkeypatch):  
	tim = BankCustomer("Tim")  

	account = BankAccount("Test", 1000)  
	tim.add_account(account)  

	monkeypatch.setattr(BankAccount, "balance", 1000)  
	assert tim.total_balance == 1000
```
>This allows the test to pass without fixing the code in a different Python module
>Note that the `monkeypatch` is a fixture received as argument to the test function
## Mocks

- Monkey patching is very useful and efficient in simple cases
- It allows you to change attributes on the fly to make your tests pass
- Sometimes not possible to monkey patch specific attributes, and you need to replace your  entire classes
- Sometimes you may want to change the behaviour of "builtin" functions, such as `input` or `open`
- Mocks are used in this case, they are pieces of code that replace the behaviour of another piece of code
- The process of "injecting" mocks into the code is called patching
### Patching with `patch`

```
from unittest.mock import patch

@patch("builtins.input", side_effect=["abc", "def"])  
def test_example(mock_input):  
	value1 = input()  
	value2 = input()  
	assert value1 == "abc"  
	assert value2 == "def"
```

- The code patches the builtin `input` method
- It replaces it with a mock (available in the test function as `mock_input`, see arguments)
- The mock has a **side effect**
	- The side effects are fake user inputs 
	- It returns "abc" the first time it is called
	- and returns "def" the second time it is called
- The `mock_input` replaces the `input` method, making it non-interactive and predictable
### Patching the `open` function

```
from unittest.mock import mock_open, patch  

FILE_CONTENTS="line1\nline2\nline3\n"  

@patch("builtins.open", new_callable=mock_open, read_data=FILE_CONTENTS)  
def test_open(mock_file):  
	with open("my_file.txt", "r") as fp:  
		data = [line.strip() for line in fp.readlines()]  

	assert data[0] == "line1"  
	assert data[1] == "line2"
```

- Very common to patch the `open` method in Python
- The tests should not depend on local files whose content you don't control
- Unit tests will patch `open` to control the "content" on which the program operates
- It can be complicated to create a mock object every time - especially because `open` is a standalone function, but can also be used as a context manager (`with open ...`)
- Python comes with a preexisting mock called `mock_open`
- Use it in combination with `patch`