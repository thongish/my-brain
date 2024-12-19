## app.py
```
from flask import Flask, render_template, request, jsonify
from db import db
from pathlib import Path
from models import Book, BookRental, Category, User
from datetime import datetime

app = Flask(__name__)

app.config["SQLALCHEMY_DATABASE_URI"] = "sqlite:///bookstore.db"
app.instance_path = str(Path(".").resolve())

db.init_app(app)
@app.route("/")
def home():
    random = "This is my home page"
    return render_template("base.html", text=random)

# BOOK STUFF STARTS HERE ---------------------------------------------------------------

@app.route("/books")
def books():
    statement = db.select(Book)
    books = db.session.execute(statement).scalars()

    return render_template("books.html", books=books)

@app.route('/books/<int:id>')
def book_id(id):
    statement = db.select(Book).where(Book.id == id)
    book = db.session.execute(statement).scalar()

    error = "BOOK NOT FOUND!"
    if not book:
        return render_template("base.html", text=error), 404
    return render_template("book_info.html", book=book)

# USER STUFF STARTS HERE ---------------------------------------------------------------

@app.route("/users")
def users():
    statement = db.select(User)
    users = db.session.execute(statement).scalars()

    return render_template("users.html", users=users)

@app.route('/user/<int:id>')
def user_id(id):
    statement = db.select(User).where(User.id == id)
    user = db.session.execute(statement).scalar()

    error = "USER NOT FOUND!"
    if not user:
        return render_template("base.html", text=error), 404
    return render_template("unique_user.html", user=user)

# CATEGORY STUFF STARTS HERE ---------------------------------------------------------------

@app.route("/categories")
def categories():
    statement = db.select(Category)
    categories = db.session.execute(statement).scalars()

    return render_template("categories.html", categories=categories)

@app.route("/categories/<string:name>")
def category_detail(name):
    statement = db.select(Book).where(Book.category.has(Category.name == name))
    books = db.session.execute(statement).scalars()

    # This is so I can display category name on the html page
    category_statement = db.select(Category).where(Category.name == name)
    category = db.session.execute(category_statement).scalar()

    error = "CATEGORY NOT FOUND!"
    if not category:
        return render_template("base.html", text=error), 404
    return render_template("category_books.html", books=books, category=category)

# RENTING STUFF STARTS HERE ---------------------------------------------------------------

@app.route('/available')
def available():
    # statement = db.select(Book).where(~Book.rentals.any() | Book.rentals.any() & ~Book.rentals.any(BookRental.returned_on == None)).order_by(Book.title)
    statement = db.select(Book).where(~Book.rentals.any() | ~Book.rentals.any(BookRental.returned_on == None)).order_by(Book.title)
    books = db.session.execute(statement).scalars()

    return render_template("available.html", books=books)

@app.route('/rented')
def rented():
    book_ids_stmt = db.select(BookRental.book_id).where(BookRental.rented_on < datetime.now()).where(BookRental.returned_on == None)
    book_ids = [id for id in db.session.execute(book_ids_stmt).scalars()]
    ordered_books = db.select(Book).where(Book.id.in_(book_ids)).order_by(Book.title)
    books = db.session.execute(ordered_books).scalars()

    return render_template("rented.html", books=books)

# API STUFF STARTS HERE ---------------------------------------------------------------

@app.route("/api/books")
def return_books():
    statement = db.select(Book)
    book_execute = db.session.execute(statement).scalars()

    books = []
    for book in book_execute:
        books.append(book.to_dict())

    return jsonify(books)

@app.route("/api/books", methods=["POST"])
def create_book():
    data = request.get_json()

    # Validation functions
    is_positive_number = lambda num: isinstance(num, (int, float)) and num >= 0
    is_non_empty_string = lambda s: isinstance(s, str) and len(s) > 0
    is_valid_rating = lambda num: isinstance(num, int) and 1 <= num <= 5

    # Field mapping
    required_fields = {
    "title": is_non_empty_string,
    "price": is_positive_number,
    "available": is_positive_number,
    "rating": is_valid_rating,
    "url": is_non_empty_string,
    "upc": is_non_empty_string,
    "category": is_non_empty_string,
    }

    # Field validation
    for field in required_fields:
    # The field is missing
        print(field)
        if field not in data:
            return {"error": f"Missing field: {field}"}, 400
        else:
            # Extract the validation function
            func = required_fields[field]
            # Extract the value
            value = data[field]
            # Validate the value
            if not func(value):
                return {"error": f"Invalid value for field {field}: {value}"}, 400

    # Check if upc already exists in book table
    book_statement = db.select(Book.upc)
    book_execute = db.session.execute(book_statement).scalars()
    book_upc = []
    for upc in book_execute:
        book_upc.append(upc)
    if data["upc"] in book_upc:
        return {"error": "UPC of this book already exists in the book records"}, 400

    # Check if category already exists
    category_name = data.pop("category")
    category_statement = db.select(Category).where(Category.name == category_name)
    category_execute = db.session.execute(category_statement).scalar()
    if not category_execute:
        # create new category object
        category_object = Category(name=category_name)
    else: 
        # use existing category object
        category_object = category_execute

    category_col = {}
    category_col["category"] = category_object

    book = Book(**data,**category_col)
    db.session.add(book)
    db.session.commit()

    return jsonify(data)

@app.route("/api/books/<int:BOOK_ID>")
def display_book_json(BOOK_ID):
    book_statement = db.select(Book).where(Book.id == BOOK_ID)
    book_execute = db.session.execute(book_statement).scalar()

    # Checking if the book is available
    available = False
    if book_execute.rentals:
        for rental in book_execute.rentals:
            if not rental.returned_on:
                available = False
            else:
                available = True
    else: 
        available = True

    book = book_execute.to_dict()
    book.update({"available":available})

    return jsonify(book)

@app.route("/api/books/<int:book_id>/rent", methods=["POST"])
def rent_book(book_id):
    data = request.get_json()
    book = db.select(Book).where(Book.id == book_id)
    bookexecute = db.session.execute(book).scalar()

    if not bookexecute:
        return "Error: this book does not exist", 404

    # Checking if the book is available
    available = False
    if bookexecute.rentals:
        for rental in bookexecute.rentals:
            if not rental.returned_on:
                available = False
            else:
                available = True
    else: 
        available = True

    if not available:
        return "Error forbidden", 403
    else:
        br = BookRental(user_id=data["user_id"], book_id=book_id, rented_on=datetime.now())
        db.session.add(br)
        db.session.commit()

    return f"Book rented on {datetime.now()}"

@app.route("/api/books/<int:book_id>/return", methods=["PUT"])
def return_book(book_id):
    statement = db.select(BookRental).where(BookRental.book_id == book_id).where(BookRental.returned_on == None)
    execute = db.session.execute(statement).scalar()

    if not execute:
        return "Error: Book has not been rented", 403

    # Giving value to returned_on column
    execute.returned_on = datetime.now()
    db.session.commit()

    book = execute.to_dict()

    return jsonify(book)

if __name__ == "__main__":
    app.run(debug=True, port=8888)
```

## db.py
```
from flask_sqlalchemy import SQLAlchemy
from sqlalchemy.orm import DeclarativeBase

class Base(DeclarativeBase):
    def to_dict(self):
        book = {}

        # used your code but made it more readable for myself
        for field in self.__table__.columns:
            book[field.name] = getattr(self, field.name)

        return book

db = SQLAlchemy(model_class=Base)
```

## models.py
```
from db import db
from sqlalchemy.orm import relationship, mapped_column
from sqlalchemy import ForeignKey, String, Integer, DateTime, DECIMAL

class Book(db.Model):
    id = mapped_column(Integer, primary_key=True)
    upc = mapped_column(String) 
    title = mapped_column(String)
    price= mapped_column(DECIMAL(10,2))
    available = mapped_column(Integer, default=0)
    url = mapped_column(String)
    rating = mapped_column(Integer, default=0)
    category_id = mapped_column(Integer, ForeignKey("category.id"))
    category = relationship("Category", back_populates="books")
    rentals = relationship("BookRental", back_populates="book")

class Category(db.Model):
    id = mapped_column(Integer, primary_key=True)
    name = mapped_column(String)
    books = relationship("Book", back_populates="category")

class User(db.Model):
    id = mapped_column(Integer, primary_key=True)
    name = mapped_column(String)
    rented = relationship("BookRental", back_populates="user")

class BookRental(db.Model):
    id = mapped_column(Integer, primary_key=True)
    user_id = mapped_column(Integer, ForeignKey("user.id"))
    book_id = mapped_column(Integer, ForeignKey("book.id"))
    rented_on = mapped_column(DateTime(timezone=True), nullable=False)
    returned_on= mapped_column(DateTime(timezone=True), nullable=True)
    user = relationship("User", back_populates="rented")
    book = relationship("Book", back_populates="rentals")
```

## manage.py
```
from db import db
from models import Category, Book, User, BookRental
from sqlalchemy import select
from sqlalchemy.sql import func
import csv
from app import app
from datetime import datetime

def create_db():
    db.drop_all()
    db.create_all()

def import_books():
    with open("./data/books.csv", "r") as fp:
        reader = csv.DictReader(fp)

        for book in reader:
            book_category = book["category"]
            book.pop("category")
            possible_category = db.session.execute(select(Category).where(Category.name == book_category)).scalar()
            # print(possible_category)
            if not possible_category:
                category_object = Category(name=book_category)
                db.session.add(category_object)
            else:
                category_object = possible_category

            row = {}
            row["category"] = category_object

            book_object = Book(**book, **row)
            db.session.add(book_object)

        db.session.commit()

def import_users():
    with open("./data/users.csv", "r") as fp:
        reader = csv.DictReader(fp)

        for user in reader:
            user_object = User(name=user["name"])
            db.session.add(user_object)

        db.session.commit()

def import_rentals():
    with open("./data/bookrentals.csv", "r") as fp:
        reader = csv.DictReader(fp)

        for rental in reader:
            book_statement = db.select(Book).where(Book.upc == rental["book_upc"])
            book = db.session.execute(book_statement).scalar()

            user_statement = db.select(User).where(User.name == rental["user_name"])
            user = db.session.execute(user_statement).scalar()

            if book and user and rental["returned"]:
                rental_object = BookRental(user_id=user.id,
                                            book_id=book.id,
                                             rented_on=datetime.strptime(str(rental["rented"]), "%Y-%m-%d %H:%M"),
                                              returned_on=datetime.strptime(str(rental["returned"]), "%Y-%m-%d %H:%M"))
                db.session.add(rental_object)

            elif book and user:
                rental_object = BookRental(user_id=user.id,
                                            book_id=book.id,
                                             rented_on=datetime.strptime(str(rental["rented"]), "%Y-%m-%d %H:%M"))
                db.session.add(rental_object)
            db.session.commit()

with app.app_context():
    create_db()
    import_books()
    import_users()
    import_rentals()
```

## book_info.py
```
{% extends "base.html" %}

{% block content %}
<h1>{{ book.title }}</h1>
{% if book.rentals %}
    {% for rental in book.rentals %}
    <div>
        <div class="card">
            <div class="card-body">
                <p class="card-text">Rented by: {{ rental.user.name }}</p>
                <p class="card-text">Rented on: {{ rental.rented_on.strftime("%Y-%m-%d %H:%m") }}</p>
                <p class="card-text">{% if rental.returned_on %}Returned on: {{ rental.returned_on.strftime("%Y-%m-%d %H:%m") }}{% endif %}</p>
            </div>
        </div>
    </div>
    {% endfor %}
{% else %}
    <div>
        <div class="card">
            <div class="card-body">
                <p class="card-title">Book never been rented b4</p>
            </div>
        </div>
    </div>
{% endif %}
{% endblock %}
```