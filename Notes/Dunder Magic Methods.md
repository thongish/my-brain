#OOP/W5

# Python built-in methods

- Everything in Python is an object
	- The base type (class) in Python is `{python}object`
- Python defines several built-in methods
	- enclosed by `{python}__`: the "**dunder**" - double underscore
- `{python}__init__` is the constructor (initializes values)
- There are other ones:
	- `{python}__new__` - the actual "constructor", outside the scope of this course
	- `{python}__str__` - returns a string representation of the object
- Dunder methods are **magic** because they are run without being called explicitly

## Example: the `{python}Person` class

```python
class Person:  
	def __init__(self, name):  
		self._name = name  
		
	def __str__(self):  
		return f"Person: {self._name}"
```

- `{python}__str__` will be called when casting the object into a string 
	- For example, in a `{python}print` statement, or when using `{python}str(my_instance)`
```python
tim = Person("Tim")

print(tim)
# Also possible: str(tim)
```

# Other useful methods to override

- `{python}instance` is an instance of the class considered

| Method                              | Goal                                                      |
| ----------------------------------- | --------------------------------------------------------- |
| `{python}__str__(self)`             | For `{python}print(instance)` or `{python}str(instance)`  |
| `{python}__len__(self)`             | Allows `{python}len(instance)`                            |
| `{python}__getitem__(self,key)`     | Allows `{python}instance[value]` (can be a slice)         |
| `{python}__call__(self)`            | Allows to use `{python}instance()`                        |
| `{python}__contains__(self, other)` | Allows to test `{python}something in instance` expression |
| `{python}__iter__(self)`            | Allows to use `{python}instance` as an iterator           |
| `{python}__next__(self)`            | Returns the next value in the iteration (see above)       |
# Dunder "mathematical" methods

Here’s the information formatted in a markdown table:

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
# Implementing the `{python}__lt__` method for the Score class

```python
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
```python
scores = [Score("Tim", 0), Score("John", 1000), Score("Sarah", 2000)]  
print(sorted(scores)) # Will display the sorted result  
scores.sort()         # Will sort in place
```

# Design pattern: using collections

The high scores board is a **collection** of scores
```python
class HighScores:  
	def __init__(self):  
		self._scores = list()  
	# We would need to manage scores here, or use aggregation  
	def __len__(self):  
		return len(self._scores)
```

And then:
```python
hiscores = HighScores()
hiscores.add(tim_score)
len(hiscores) # will return 1 (1 score in the list)
```

# Using `{python}operator` for sorting (and other things)

- Python standard library comes with the `{python}operator` module
- Provides premade functions to access:
	- items
	- elements of an object
	- collection
- `{python}itemgetter` - to get items from lists/dictionaries by key (index for a list or key for a dictionary)
- `{python}attrgetter` - to get attributes from objects (by attribute name)

**With lists**
```python
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
```python
menu = [  
	{ "name": "pizza", "price": 10, "in stock": 10 },  
	{ "name": "drink", "price": 2, "in stock": 50 },  
	{ "name": "cookie", "price": 4, "in stock": 20 },  
	{ "name": "pizza slice", "price": 3, "in stock": 15 },  
]  
sorted(menu, key=operator.itemgetter('price'))
```

**With objects**
```python
hiscores = [  
	Score(name="Tim", score=20),  
	Score(name="John", score=0),  
	Score(name="Sarah", score=100),  
]  
# Sorting on the name attribute  
sorted(hiscores, key=operator.attrgetter('name'))
```

# Collections: getting elements with `{python}__getitem__`

```python
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