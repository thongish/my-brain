# Variable number of arguments

- There are situations where a function can take a variable number of arguments
- Or situations where all arguments to a specific function call are already available in a dictionary or a list
- Python has a mechanism for "unpacking" these arguments
- Syntax is `*args` (for iterables) and `**kwargs` (for dictionaries)
# Review: positional and keyword arguments

Functions take positional and keyword arguments. Typical way to use them:
```
def func(pos1, pos2, pos3, keyword1="value1", keyword2=None, keyword3=42)
	pass
```
- `pos1`, `pos2`, `pos3` are _positional_ arguments
	- they are **required**
	- don't have to provide names when calling function
	- `func(1, "b", None)` is a valid call
- `keyword1`, `keyword2`, `keyword3` are _keyword_ arguments
	- they are **not required**
	- if not provided, they take default values
- Positional arguments always come **before** keyword arguments
- `*args` is a **list** of positional arguments
- `**kwargs*` is a **dictionary** of keyword/value arguments/parameters
### Example: iterable
```
def func(*args):
	print(args)

func("yes", 2) # prints ["yes", 2]
```
### Example: dictionary
```
def func(**kwargs):
	print(kwargs)
	
func(example="yes", value=2) # prints {"example": "yes", "value": 2}
```
### Works both ways
```
my_list = ["yes", 2]
my_dict = {"example": "yes", "value": 2}

func(*my_list)    # equivalent to func("yes", 2)
func(**my_dict)   # equivalent to func(example="yes", value=2)
```
### You can combine them
```
func("example", *my_list, keyword1="value1", **my_dict)
```
### Use it wisely
- Extremely powerful way of dealing with variable / multiple arguments
```
kwargs = {}
if difficulty in ("easy", "medium", "hard"):
	kwargs["difficulty"] = difficulty
	
if category in get_categories():
	kwargs["category"] = category
	
if number.isdigit():
	kwargs["number"] = int(number)
	
get_questions(**kwargs)
```