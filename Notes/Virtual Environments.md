#OOP/W1
# Why venvs are useful

- Allows separation of  dependencies between projects
	- Useful if projects require different versions of libraries or packages
- Isolate global environment
	- Installing packages globally can affect all of your python projects
	- Can lead to compatibility issues
- Makes reproducing program environment easier
# Best practices

- Use `{python}venv` module from Python
- Created one venv per project/assignment
	- Create using `{bash}py -m venv venv`
		- This uses the module `{python}venv` and creates folder called `{python}venv`
		- `{bash}py -m venv folder`
- The venv will be created in a folder
	- Will contain binaries (scripts)
	- Will contain libraries required by the program to run
	- Folder typically called `{python}venv`
- The venv must be **activated** in order to work
	- Activate using `{python}activate` script in `{python}venv/Scripts`
- Once venv is active, the **only** commands needed are `python` and `pip`
- Don't use `py`, `python3`, etc.

# [[2515 Week 1]]