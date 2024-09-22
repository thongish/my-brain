#OOP/W2 
# Definitions

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
	- Python does not have it, but you can use `{python}_` in the beginning of the attribute to mean it is private
- Using private attributes and using methods to change the state is called **encapsulation**

# Abstraction

- The implementation of behaviours of the object is the responsibility of the class
- Other objects should not depend upon private attributes or methods
- They should only use the public interface of the class (the public methods and attributes)
- Process of hiding the internal details of an application from the outer world
	- ex. I know how to call and use the string method `{python}string.upper()` but I don't know the inner working of why and how it does what it does

# Class syntax in Python

- `{python}class MyClassName:` to define a new class "block"
- Except for class variables, a class definition only has **methods**
- Methods are defined inside the class block, and receive `{python}self` as first parameter
- A special method is `{python}__init__`, always called upon initialization of the instance

```python
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

# The `{python}self` parameter

- All functions within a class are called "methods"
- They receive an implicit parameter: `{python}self`, which represents the current **instance**
- This allows **encapsulation**
	- i.e. each instance has its own version of the class attributes, and they are accessed with `{python}self`
- **NEVER** use `{python}self` outside of the class block

# Parameter validation

- Imagine the `{python}student` class should not allow students with "invalid names"
- We will make it raise an exception if that is not the case

```python
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

# Using Python `{python}property`

- Python has a decorator which makes encapsulation and abstraction easier
- You can use the `{python}@property` decorator on a method, and then it will behave as an **attribute**
	- This allows you to implement getters very easily
```python
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

```python
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
	- You also need to use this name in the `{python}@[name].setter` decorator

# Static methods and class methods

- You can define methods that are common to all objects of the same class
- Static methods do not get any reference tot he class or object
- Class methods receive a reference to the **class** when called directly from the class name
- This reference is typically called `{python}cls`
- Use the `{python}@staticmethod` decorator for static methods (no reference)
- Use the `{python}@classmethod` decorator for class methods (reference to class)

## Static method example

```python
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

```python
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
- The previous example uses a class variable `{python}PROGRAMS`
- Class methods have access to class variable (but no instance variables)
- Static methods do not have access to class variables, nor instance variables

# What you REALLY need to know

- How to define a class: `{python}class MyClass:`
- Understand what the constructor does ( `{python}__init__` )  
- Understand what `{python}self` is  
- Be able to write any instance methods  
- Because you define an instance variable `{python}self.something` in`{python}__init__` ...  
	- DOES NOT MEAN that `{python}__init__` will take it as a parameter!  
- Understand what inheritance, but also understand when NOT to use it (i.e. most of the time by yourself, unless you are using a library / package)  
- In the context of this course, using class variables and class / static methods and variables is a bad idea and  almost never happens, except when working with SQLAlchemy. If you are using them, make sure you know what  you are doing.  
- There is very little to learn or know about Object Oriented Programming. It is mostly about how you "view the  world" in your program.



# Flash cards

What is a **class**?
?
- Something that defines a general category (i.e. book, bank account)
- Blueprint (or template) for creating an object
- A custom data type
---
Example:
- A book is a **class** (the abstract concept of something you can read)
- "Harry Potter" is an instance (or object) of the **book class**

What is an **object** or **instance** in the context of Python classes?::A "thing" created out of a class

What is an **attribute** in the context of Python classes?::Values for a specific object

What is a **state** in the context of Python classes?::The current values of the attributes in an object

What is **modelization** in the context of Python classes?::Creating a class based on real life objects (deciding which attributes/behaviours it has)

Making sure a class has a "clean" public interface that hides complex implementation details is called,::Abstraction

Which of the following respects the PEP8 naming convention for classes?
- my_nice_class
- MyNiceClass
- myNiceClass
- NICE_CLASS
?
MyNiceClass

What is **encapsulation**?::Ensuring the state of an object can only be changed by the object methods itself rather than changing it outside of the class

What is the implicit parameter that all functions within a class receive?::`{python}self`