#OOP/W1
# Important concepts

- Python code is written in files
- Each file is a Python module

```python
# Contents of my_print.py

MY_MESSAGE = "Hello!"

def my_print_func(text):
	print(MY_MESSAGE)
	print(text)
```
- You can import other files,
```python
# Contents of main.py
import my_print

def main():
	my_print.my_print_func("Example.")
	print(my_print.MY_MESSAGE)
```
-  The entire `{python}my_print` module is imported
- You can access functions or variables using `.` notation
	- Can also access "properties" with `.` notation
- Everything in Python is an object
- When module is imported, the code it contains is **executed**
- Make sure to use `{python}if __name__ == "__main__":` to prevent side effects

- or specific symbols of a module:
```python
from my_print import MY_MESSAGE  

print(MY_MESSAGE)
```

# Python packages

- Packages are collections of modules
- Several files in a folder
- Is a folder with `{python}__init__.py` file in it
	- can work without one, but should always have one

## About packages

- Python packages can contain modules, and other packages
```python
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

- You can import the whole package just like modules: `{python}import logic`
	- and then use `.` to access submodules/packages
```python
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

```python
import logic.game  

logic.game.start() # OK  

logic.computer.aimbot.shoot() # DOES NOT WORK (we only have logic.game)
```

## Importing and renaming

- Can be convenient for long/complicated names
```python
import logic.computer.aimbot as bot

bot.shoot()
```

## Using `{python}__init__.py` to allow easier access to subpackages

- When Python encounters an `{python}import` statement and the symbol imported is a package, the `{python}__init__.py` file will automatically run
- This file can import functions/variables from submodules and packages to allow for easier imports
```python
├── logic  
│ ├── __init__.py  
│ ├── constants  
│ │ ├── __init__.py  
│ │ ├── player.py       # Contains NUMBER_PLAYERS = 10  
│ │ └── bot.py          # Contains AIMBOT_PRECISION = 1.0  
│ └── game.py  
└── main.py
```
### `{python}logic/__init__.py`
```python
from .constants.player import NUMBER_PLAYERS  
from .constants.bot import AIMBOT_PRECISION
```
### `{python}main.py`
```python
from logic import NUMBER_PLAYERS  

# Or even  
from logic import NUMBER_PLAYERS, AIMBOT_PRECISION
```

## Packages and paths

- When running a Python program, the working directory is the **directory where you ran the Python command**
- This can have an effect when testing/developing programs
```python
├── my_package  
│ ├── __init__.py  
│ └── my_module.py  
├── file.txt  
└── main.py
```

```python
# Contents of my_package/my_module.py  
open("file.txt", "r")
```
- `python my_package/my_module.py`: WORKS
- `python -m my_package.my_module`: WORKS (preferred way)
- `cd my_package`, and then `python my_module.py`: DOES NOT WORK (there is no "main.txt" file in the `{python}my_package` folder)


# Flash Cards

```python
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
Let's say you wanted to import the aimbot module so you can use the `{python}shoot()` function. How would you do that?
?
`{python}import logic.computer.aimbot`
 


# [[2515 Week 1]]