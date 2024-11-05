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
