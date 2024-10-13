#OOP/W4 
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
- The convention in Python is to use `{python}_name` for a private variable called `{python}name`
- In UML, you use a `{python}-` for private attributes, and `{python}+` for public attributes

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

