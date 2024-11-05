# Argument Unpacking
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
# CSV: Comma Separated Values

- Typical and easy way to represent tabular data
- Use it with `import csv`
- Read from files with a `reader` (or `DictReader`)
- Write to files with a `writer` (or `DictWriter`)
```
import csv

with open("file.csv", encoding="utf-8") as fp:
	reader = csv.reader(fp) # or DictReader
	for row in reader:
		print(row)
```
### Writing CSV files

- Use `writer`, and write lists/tuples
- Better! Use `DictWriter`
	- Requires the `fields` to be provided as a list
	- Writes the header row with `.writeheader()`
	- Takes dictionaries, and write rows
```
example = {"name": "Tim", "grade": 25}
fields = list(example.keys())
with open("output.csv", "w", encoding="utf-8", newline="") as fp:
	writer = DictWriter(fp, fields=fields)
	writer.writeheader()
	writer.writerow(example)
```
# JSON: JavaScript Object Notation

- One of many ways to represent data
- Similar to the way JavaScript represents data internally
- Very heavily used for communications between clients and servers using ReSTful APIs

**Pros**:
- Lightweight and very flexible
- Language independent
- Easy to read and write (even by humans)
- Flat (text format)
**Cons**:
- Very flexible - no validation
- No comments
- Hard to "debug"
### JSON data types

- Key/value pairs
- Keys are strings
- Values can be:
	- strings
	- numbers (integer, float)
	- objects (= another JSON block)
	- arrays
	- special (bool, null)
### JSON Example
![[Pasted image 20241104153255.png]]
### JSON in Python

- Python has native support for `json`

**Definitions**:
- Serialization: creating JSON from data
- Deserialization: creating data from JSON
- The json library supports the serialization/deserialization of several Python native data types
```
import json

with open("input.json") as fp:
	json.load(fp)
	
value = """["JSON list", {"keyword": "value"}]"""
data = json.loads(value)

with open("output.json", "w") as fp:
	json.dump(data, fp)
	
print(json.dumps(data))
```
### Python - JSON mappings

| Python           | JSON    |
| ---------------- | ------- |
| dict             | object  |
| list, tuple      | array   |
| str              | string  |
| int, long, float | number  |
| boolean          | boolean |
| None             | null    |
### Using JSON to represent class instances

- There is no built in way to serialize or deserialize Python classes
- Use the built-in conversion for the Python primitive types
- Serialization: create `to_json` method that returns a JSON string
	- converts the state into a Python dict or list, serialize to JSON
	- create a `to_dict` method that returns a dictionary
- Deserialization: convert from JSON
	- create a class method `from_json` method that takes in a JSON string
	- deserialize the string to a dict or list
	- create an instance, and set the instance attributes to the values from the dict/list
# SQL Alchemy and database persistence

- SQL Alchemy is a module that makes it easy to interact with SQL databases
- Install it in your virtual environment with `pip install sqlalchemy`
- SQL Alchemy has ORM capabilities (Object Relational Mapping)
- It allows you to transform SQL rows in a table to Python objects and vice versa
- We only use SQL Alchemy 2.0
### Setting up your engine
```
from sqlalchemy import create_engine

engine = create_engine("sqlite:///bing.db", echo=True)
# set echo to False to stop seeing shit in the terminal
```
### Setting up your Session class
```
# File: database.py
from sqlalchemy.orm import sessionmaker

Session = sessionmaker(bind=engine)
```
### Always use a session!
```
from database import Session

# Option 1
session = Session()
	# do stuff
	
# Option 2
with Session() as session:
	# do stuff
```
### Create your Base class
```
from sqlalchemy.orm import DeclarativeBase

class Base(DeclarativeBase):
	pass
```
### Create a database-backed class
```
from sqlalchemy import String, DECIMAL, Integer, ForeignKey

class Book(Base):
	__tablename__ = "books"
	
	id = mapped_column(Integer, primary_key=True)
	title = mapped_column(String)
	price = mapped_column(DECIMAL(10, 2))
	available = mapped_column(Integer, default=0)
```
- You always need a primary key
- column types are defined by SQL Alchemy
### Create the tables
```
Base.metadata.create_all()
```
### Use the session to make queries (execute statements)

1. Create the statement (usually with `select`)
2. Execute the statement (`session.execute`)
3. Get the results (`.scalars()` or `.scalar()`)
```
from sqlalchemy import select

statement = select(Book)
results = session.execute(statement)
books = results.scalars()
```
### Use the session to add rows
```
book = Book(title="ACIT2515", available=10, price=22.95)
session.add(book)
book = Book(title="Other book", available=1, price=12.95)
session.commit()
```
### Use the session to delete rows
```
# Remove book with ID = 10
book = session.execute(select(Book).where(Book.id == 10)).scalar()
session.delete(book)
session.commit()
```
### Statements

- Statements are SQL-like Python objects. Useful operations include:
	- where clauses (can be combined)
		- `select(Book).where(Book.rating <= 1)`
- `select(Book).where(Book.rating >= 3).where(Book.title.ilike("%last%"))`
	- ordering
		- `select(Book).where(Book.available > 0).order_by(Book.rating)`
	- reverse ordering
		- `select(Book).order_by(Book.rating.desc()))` (SQL descending)
### Functions

Backend specific functions can be useful (for example `RANDOM`)
```
from sqlalchemy.sql import func

# Random sort using SQL RANDOM function
select(Book).where(Book.available > 0).order_by(func.random())
```
### Using results

After executing your statement, you can extract the results. Use the following methods:
- `.scalars()`: returns a list of result objects
- `.scalar()`: returns one result only
- `.first()`: returns the first object or `None`
### Relationships / foreign keys: one-to-many

- You must define a `ForeignKey` column
- The `ForeignKey` links to the `primary_key` of the other table
- Use `relationship` fields to automatically fetch the related objects

### One to many: Python code
```
class Book(Base):
	# [...] other fields
	category_id = mapped_column(Integer, ForeignKey("categories.id"))
	category = relationship("Category", back_populates="books")
	
class Category(Base):
	__tablename__ = "categories"
	
	id = mapped_column(Integer, primary_key=True)
	name = mapped_column(String)
	books = relationship("Book", back_populates="category")
```
### One to many: using `relationship` attributes
```
book = session.execute(select(Book).order_by("?")).scalar()  
# Relationship from Book to Category (one)  
print(book.category.name)  
poetry = session.execute(select(Category).where(name="Poetry")).scalar()  
# Relationship from Category to Book(s) (many)  
for book in poetry.books:  
	print(book.title)
```
### Many to many: association object

- Use an association object, with two foreign keys to each class you want to link
- Carefully name and use the `relationship` fields to set up associations
### Rental books at the library
```
class User(Base):  
	__tablename__ = "users"  
	
	id = mapped_column(Integer, primary_key=True)  
	name = mapped_column(String)  
	rentals = relationship("BookRental", back_populates="user")  
	
class BookRental(Base):  
	__tablename__ = "book_rentals"  
	
	id = mapped_column(Integer, primary_key=True)  
	user_id = mapped_column(Integer, ForeignKey("users.id"))  
	book_id = mapped_column(Integer, ForeignKey("books.id"))  
	rented_on = mapped_column(DateTime(timezone=True), nullable=False)  
	returned_on = mapped_column(DateTime(timezone=True), nullable=True)  
	user = relationship("User", back_populates="rentals")  
	book = relationship("Book", back_populates="rentals")
```
### Rent books
- Create `BookRental` instances
```
from datetime import datetime, timedelta  
tim = session.execute(select(User).where(name == "Tim")).scalar()  
book = session.execute(select(Book).where(title == "ACIT2515")).scalar() 
another_book = session.execute(select(Book).where(Book.id == 10)).scalar()  

rental1 = BookRental(user=tim, book=book, rented_on=datetime.now())  

yesterday = datetime.now() - timedelta(days=1)  
rental2 = BookRental(user=time, book=another_book, rented_on=yesterday)  

session.add(rental1)  
session.add(rental2)  

session.commit()
```
### Find unreturned books for the user `tim`
```
stmt = select(BookRental).where(BookRental.user == tim).where(BookRental.returned_on != None)  

books_not_returned = [result.book.title for result in session.execute(stmt).scalars()]
```
### Another way to do the same thing (Python side)
```
books_not_returned = []  
for rental in tim.rentals:  
	if rental.returned is None:  
		books_not_returned.append(rental.book)  

books_not_returned = [rental for rental in tim.rentals if rental.returned_on is None]
```
### Find all the "Travel" books `tim` ever rented
```
travel = session.execute(select(Category).where(Category.name == "Travel")).scalar()  

stmt = select(BookRental).where(BookRental.user == tim).where(BookRental.book.has(category=travel))  

results = session.execute(stmt).scalars()  

for association in results:  
	print(association.book.title)
```
### Find all the people who rented a specific book with the dates
```
book = session.execute(select(Book).where(Book.title == "ACIT2515")).scalar()  

for rental in book.rentals:  
	print(rental.user.name, rental.rented_on, rental.returned_on)
```
# My database part 1
```
# db.py

from sqlalchemy import create_engine
from sqlalchemy.orm import sessionmaker

engine = create_engine("sqlite:///something.db", echo=False)
Session = sessionmaker(bind=engine)

# models.py

from sqlalchemy.orm import DeclarativeBase, relationship
from sqlalchemy.orm import mapped_column
from sqlalchemy import ForeignKey, String, DECIMAL, Integer

class Base(DeclarativeBase):
    pass

class Book(Base):
    __tablename__ = "books"

    upc = mapped_column(String, primary_key=True)
    title = mapped_column(String)
    price= mapped_column(DECIMAL(10,2))
    available = mapped_column(Integer, default=0)
    url = mapped_column(String)
    rating = mapped_column(Integer, default=0)
    category_id = mapped_column(Integer, ForeignKey("categories.id"))
    category = relationship("Category", back_populates="books")

class Category(Base):
    __tablename__ = "categories"

    id = mapped_column(Integer, primary_key=True)
    name = mapped_column(String)
    books = relationship("Book", back_populates="category")

# main.py

import csv
from models import Book, Base, Category
from db import Session, engine
from sqlalchemy import select
import sys

if __name__ == "__main__":

    if len(sys.argv) > 1:
        if sys.argv[1] == "import":

            Base.metadata.drop_all(engine)
            Base.metadata.create_all(engine)

            with open("books.csv", "r") as fp:
                reader = csv.DictReader(fp)
                session = Session()

                for book in reader:
                    book_category = book["category"]
                    book.pop("category")
                    possible_category = session.execute(select(Category).where(Category.name == book_category)).scalar()
                    print(possible_category)
                    if not possible_category:
                        category_object = Category(name=book_category)
                        session.add(category_object)
                    else:
                        category_object = possible_category

                    row = {}
                    row["category"] = category_object

                    book_object = Book(**book, **row)
                    session.add(book_object)
                session.commit()

```
# Tim's database part 1
```
# models.py

from sqlalchemy import String, DECIMAL, Integer, ForeignKey, DateTime
from sqlalchemy.orm import mapped_column, relationship
from sqlalchemy.orm import DeclarativeBase


class Base(DeclarativeBase):
    def to_dict(self):
        """Convenience method to serialize any object - omit the ID column"""
        return {
            field.name: getattr(self, field.name)
            for field in self.__table__.columns
            if field.name != "id"
        }


class Book(Base):
    __tablename__ = "books"

    id = mapped_column(Integer, primary_key=True)
    title = mapped_column(String)
    price = mapped_column(DECIMAL(10, 2))
    available = mapped_column(Integer, default=0)
    rating = mapped_column(Integer, default=0)
    url = mapped_column(String)
    upc = mapped_column(String, default=0)
    category_id = mapped_column(Integer, ForeignKey("categories.id"))
    category = relationship("Category", back_populates="books")


class Category(Base):
    __tablename__ = "categories"

    id = mapped_column(Integer, primary_key=True)
    name = mapped_column(String)
    books = relationship("Book", back_populates="category")

# main.py

import csv
from pathlib import Path
import sys
from models import Base, Book, Category
from db import engine, Session

from sqlalchemy import select

def delete_database():
    Path("bing.db").unlink(missing_ok=True)
    print("!! DELETED THE DATABASE FILE")

def create_tables():
    Base.metadata.create_all(engine)
    print("-- CREATED TABLES")

class Importer:
    def __init__(self, filename="books.csv"):
        self.session = Session()
        self.filename = filename
        self.load_data_from_csv()

    def get_category_by_name(self, name):
        stmt = select(Category).where(Category.name == name)
        possible = self.session.execute(stmt).scalar()

        return possible

    def get_or_create_category(self, name):
        possible = self.get_category_by_name(name)
        # The category exists in the database
        if possible:
            return possible

        # If it does not, create it
        category = Category(name=name)
        self.session.add(category)
        return category

    def load_data_from_csv(self):
        with open(self.filename, "r", encoding="utf-8") as fp:
            reader = csv.DictReader(fp)
            for row in reader:
                # Remove the category name from the dictionary
                category = row.pop("category")
                # Replace it with the category object
                row["category"] = self.get_or_create_category(category)
                # Create the Book object using dictionary unpacking
                book = Book(**row)
                self.session.add(book)

        self.session.commit()

if __name__ == "__main__":
    if len(sys.argv) < 2:
        print(f"Use: {sys.argv[0]} reset|load|nop")
        action = "nop"
    else:
        action = sys.argv[1]

    if action == "reset":
        delete_database()
        create_tables()
    elif action == "load":
        Importer("books.csv")
    elif action == "nop":
        # Good for debugging with interactive shell
        session = Session()
        books = list(session.execute(select(Book).limit(5)).scalars())

```