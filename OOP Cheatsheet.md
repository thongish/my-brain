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
---
- A car "system" is made of a car and a driver
- A car is made of an engine and a body
	- If the car is destroyed, the driver still exists
	- If the car is destroyed, the engine does not exist anymore

![[Pasted image 20241007125821.png]]

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
\
- Very common to patch the `open` method in Python
- The tests should not depend on local files whose content you don't control
- Unit tests will patch `open` to control the "content" on which the program operates
- It can be complicated to create a mock object every time - especially because `open` is a standalone function, but can also be used as a context manager (`with open ...`)
- Python comes with a preexisting mock called `mock_open`
- Use it in combination with `patch`