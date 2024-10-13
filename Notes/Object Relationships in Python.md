#OOP/W4

You create an aggregation/composition relationship by keeping a "reference" from one object to another
# Composition

- Example: a hand **has** 5 fingers
- We choose to use a composition relationship
```python
class Finger:  
	def flick(self):  
		print("Oh no.")  
		
class Hand:  
	def __init__(self):  
		self._fingers = [Finger() for _ in range(5)]  
		
	def thumbs_up(self):  
		self._fingers[0].flick()
```
- The `{python}Finger` objects are created by the `{python}Hand` objects (when the `{python}Hand` disappears, so do the fingers)
- The `{python}Hand` can keep track and interact with the `{python}Finger` objects through the private variable `{python}self._fingers`:`{python}self._fingers[2].flick()

# Aggregation

- Example: the car and the driver
```python
class Driver:  
	def __init__(self, name):  
		self.name = name  
		
class Car:  
	def __init__(self, driver):  
		self._driver = driver
```
- You can associated the objects when creating the car:
```python
tim = Driver("Tim")
my_car = Car(Tim)
my_car = Car(driver=tim) # also works
```

# Composition and Aggregation

- In general, in a composition relationship, composite objects are created when the main object is created (in the `{python}__init__` method)
	- Can also happen elsewhere (`{python}def add_finger(self)`)
- In aggregation relationships there are usually methods in the public interface that allow you to associate/disassociate objects
	- Can be sometimes related to setters
```python
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

```python
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
- You can travel up the inheritance tree by using `{python}super()`
	- `{python}super()` will give access to the parent class (and its methods/attributes)

```python
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

```python
class Grades(list): # Grades derives from builtin `list`  
	@property 
	def average(self):  
		return sum(self)/len(self)
		  
grades = Grades([83, 90, 74, 23])  
print(grades.average) # 67.5
```

**Combine them with other objects**
```python
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

```python
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

```python
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
- `{python}animal` can be a cow or a dog, but it has an interface that defines `{python}sound()`
- from the Python interpreter perspective, `{python}animal` is just an object that happens to have a matching method available
- Note that `{python}isinstance(daisy, Animal)` returns `{python}True` even though daisy is a cow
	- Because `{python}Cow` is a child class of `{python}Animal`
	- A cow is also an animal

# Defining abstract methods in Python with `@abstractmethod` and `ABC`

```python
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