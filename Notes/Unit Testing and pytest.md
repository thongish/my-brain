#OOP/W1
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

# [[2515 Week 1]]
