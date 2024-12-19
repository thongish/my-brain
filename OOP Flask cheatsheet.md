# What is Flask?

- Flask is a microframework: does most of the heavy work dealing with HTTP requests/responses
- It has additional support for automatic JSON serialization / deserialization
- All you need is:
```
from flask import Flask
app = Flask(__name__)
if __name__ = "__main__":
	app.run(debug=True)
```
# Working with Flask: routes

- To work with your application, use the decorator `@app.route("/something")`
- The return value of the function will be sent as the HTTP response
```
@app.route("/example")
def example():
	return "I am running Flask!"
```
# Templates

- Impractical to render the a whole HTML page in the `return` statement of a route
- Better to use `render_template()` method
- `render_template("my_template.html", variable1=value1)`
- Flask will look for `my_template.html` in the templates folder
- In that template, all references to `{{ variable1 }}` will be replaced by `value1`
```
# templates/base.html
<html>
	<body>
		Hello, {{ username }}! Here are some numbers from 1 to 5:
		<ul>{% for x in range(1,6) %}<li>{{ x }}</li>{% endfor %}</ul>
	</body>
<html>
```

```
# app.py
from flask import Flask
app = Flask(__name__)
@app.route("/")
def homepage():
	return render_template("base.html", username="John doe")
if __name__ == "__main__":
	app.run()
```
# Use dictionary unpacking
```
render_template("index.html", var1=value1, var2=value2)
# The following is better and easier to manage
context = {"var1": value1, "var2", value2}
render_template("index.html", **context)
```
# Routes with arguments

- You may want to define a route that takes an argument
- For instance `/sutdent/1234` that displays information about student 1234
```
@app.route("/student/<int:student_id>")
def show_student(student_id):
	return render_template(...)
```

| Item   | Type                                         |
| ------ | -------------------------------------------- |
| string | Default type: accepts any text without slash |
| int    | Positive integers                            |
| float  | Positive integers                            |
| path   | Like strings, but accepts slashes            |
| uuid   | Accepts UUID strings                         |
# Reversing URLs in templates or Python code

In Python:
```
from flask import url_for
link = url_for("show_student", student_id=1234)
```

In a Jinja template:
```
<a href="{{ url_for ("show_student", student_id=1234)}}">Student 1234</a>
```
# Template scaffolding

- You can create reusable templates
- Generally, there is a "base" template that other templates can build on 
```
<html>
<head><title>Example</title></head>
<body><div class="container">
{% block main %}
{% endblock %}
</html>
```
# Child templates

```
# templates/home.html
{% extends "base.html" %}
{% block main %}
<h1>Welcome to my Flask website</h1>
{% endblock %}
```

```
#templates/student.html
{% extends "base.html" %}
{% block main %}
<h1>Student {{ student_id }}</h1>
{% endblock %}
```
# HTTP error codes with Flask

- In a view, you can also return a tuple:
	- the first element is the response
	- the second element is the status code
```
@app.route('/data/<value>')
def show_data(value):
	if value == "notfound":
		# We specify the status code in the return value
		return render_template('error.html'), 404
	else:
		# By default, Flask uses 200 (or 204)
		return render_template('page.html')
```

---
# Rest APIs

**Definitions**
- Representational State Transfer
- Used in most of the modern APIs on the web
- Used to support modern single page web applications
- API = Application Programming Interface
- ReST API: API to store/manage/retrieve data
- uses HTTP (protocol for web communications)
## Resources and actions

- An API allows users to access "resources" (data)
- A resource is represented by a URI (Uniform Resource Identifier)
- Resources are nouns, for example `students`
- Example: `https://my_api.com/students/2` is the URI that allows to manipulate data about the resource "student #2"
- Actions can be performed on resources
- The HTTP protocol defines several actions when accessing resources
- The 4 most important ones are:

| Action                   | HTTP verb |
| ------------------------ | --------- |
| Retrieve resource        | GET       |
| Create new resource      | PUT       |
| Update existing resource | POST      |
| Delete resource          | DELETE    |
# HTTP response codes

- The server returns a status code with the response. The status code contains information about the request and whether it was successfully processed
- The status code is a 3-digit number

| Code | Type          | Comment                                                           |
| ---- | ------------- | ----------------------------------------------------------------- |
| 1xx  | informational | request received, continuing process                              |
| 2xx  | successful    | request was successfully received, understood, and accepted       |
| 3xx  | redirection   | further action needs to be taken in order to complete the request |
| 4xx  | client error  | the request contains bad syntax or cannot be fulfilled            |
| 5xx  | server error  | the server failed to fulfill an apparently valid request          |
#### HTTP status codes need to know

| Code                      | Comment                                              |
| ------------------------- | ---------------------------------------------------- |
| 200 OK                    | everything is fine                                   |
| 204 OK                    | everything is fine (empty response)                  |
| 400 Bad Request           | the client did something wrong                       |
| 403 Forbidden             | Access to this resource is forbidden                 |
| 404 Resources Not Found   | This resource does not exist                         |
| 405 Method Not Allowed    | The resource can not be manipulated with that method |
| 500 Internal Server Error | You should be worried - bug in the application?      |
# Making HTTP request with the request library

- install it in the venv: `pip install requests`
- You can make GET, POST, PUT, DELETE requests with the relevant methods
- The following are examples using a demo API that gives you info about the request just made
### Example: GET
```
>>> response = requests.get("https://httpbin.org/get")
>>> response.text
'{\n "args": {}, \n "headers": {\n "Accept": "*/*", \n "Accept-Encoding": "gzip, deflate", \n
"Host": "httpbin.org", \n "User-Agent": "python-requests/2.24.0", \n
"X-Amzn-Trace-Id": "Root=1-5f948529-1af85529337c3efc7189b2f3"\n }, \n
"origin": "172.103.147.11", \n "url": "https://httpbin.org/get"\n}\n'
>>> response.json()
{'args': {},
	'headers': {'Accept': '*/*', 'Accept-Encoding': 'gzip, deflate',
		'Host': 'httpbin.org', 'User-Agent': 'python-requests/2.24.0',
		'X-Amzn-Trace-Id': 'Root=1-5f948529-1af85529337c3efc7189b2f3'},
		'origin': '172.103.147.11', 'url': 'https://httpbin.org/get'
}
```
### Example: PUT JSON data
```
>>> response = requests.put("https://httpbin.org/put", json={"hello": "world", "something": 12345})
>>> response.json()
{'args': {},
	'data': '{"hello": "world", "something": 12345}',
	'files': {}, 'form': {},
	'headers': {
		'Accept': '*/*', 'Accept-Encoding': 'gzip, deflate',
		'Content-Length': '38', 'Content-Type': 'application/json',
		'Host': 'httpbin.org', 'User-Agent': 'python-requests/2.24.0',
		'X-Amzn-Trace-Id': 'Root=1-5f948572-6f73cf4c41406d523a3eb244'
	},
	'json': {'hello': 'world', 'something': 12345},
	'origin': '172.103.147.11', 'url': 'https://httpbin.org/put'
}
```
- note the `data` attribute: this is what we sent to the API
### Example: status codes
- The HTTPBIN API allows us to try out status codes as well
```
>>> response = requests.get("https://httpbin.org/status/404")
>>> response.status_code
404
>>> response = requests.get("https://httpbin.org/status/503")
>>> response.status_code
503
```
## Making HTTP requests with httpie

- Install: `pip install httpie`
- You can make requests from the command line with the `http` command
```
> http get https://httpbin.org/get  
HTTP/1.1 200 OK  
Access-Control-Allow-Credentials: true  
Access-Control-Allow-Origin: *  
Connection: keep-alive  
Content-Length: 298  
Content-Type: application/json  
Date: Sat, 24 Oct 2020 19:55:09 GMT  
Server: gunicorn/19.9.0  
{  
	"args": {},  
	"headers": {  
		"Accept": "*/*",  
		"Accept-Encoding": "gzip, deflate",  
		"Host": "httpbin.org",  
		"User-Agent": "HTTPie/2.2.0",  
		"X-Amzn-Trace-Id": "Root=1-5f94869d-187ce78308c9cb23422797dc"  
		},  
	"origin": "172.103.147.11",  
	"url": "https://httpbin.org/get"  
}
```
### PUT requests with httpie

- Specify the `--json` option, use `put` for the HTTP method, and pass your values as `key=value` parameters:
```
> http --json put https://httpbin.org/put name=Tim score=1234
HTTP/1.1 200 OK
Content-Type: application/json
Server: gunicorn/19.9.0
{
	[...]
	"data": "{\"name\": \"Tim\", \"score\": \"1234\"}",
	[...]
	"json": {
		"name": "Tim",
		"score": "1234"
	},
}
```
- note how `data` has the quotes `"` characters escaped

---
# REST API with Flask

## Return JSON with Flask

- Use `jsonify` to automatically return JSON data in your views
```
@bp.route("/api/list/")  
def show_list():  
	list_of_dicts = [  
		{  
		"name": "Tim",  
		"city": "Vancouver",  
		},  
		{  
		"name": "John",  
		"city": "Toronto",  
		}  
	]  
	return jsonify(list_of_dicts)
```
## Serialize/deserialize data

- Some data types cannot be serialized natively into JSON
- You must serialize them first
- Typically using dictionaries (attributes/values)
```
@bp.route("/api/list/")  
def show_list():  
	manager = ObjectManager()  
	list_of_objects = [  
		obj.to_dict() for obj in manager.get_objects()  
	]  
	return jsonify(list_of_objects)
```
## Process arguments and parameters

```
@bp.route("/api/detail/<int:number>/")  
def show_detail(number):  
	# Return data for that specific number  
	pass
```

```
from flask import request  
@bp.route("/api/list/")  
	def show_list():  
	order = request.args.get("order", False)  
	# Will match when the request is /api/list?order=yes  
	if order == 'yes':  
		list_of_objects.sort()  
	return jsonify(list_of_objects)
```

---

# MY FLASK APP

### app.py
```
from flask import Flask, render_template
from db import db
from pathlib import Path
from models import Book, BookRental, Category, User
from datetime import datetime, timedelta


app = Flask(__name__)

app.config["SQLALCHEMY_DATABASE_URI"] = "sqlite:///bookstore.db"
app.instance_path = str(Path(".").resolve())

db.init_app(app)
@app.route("/")
def home():
    random = "This is my home page"
    return render_template("base.html", text=random)

@app.route("/books")
def books():
    statement = db.select(Book)
    books = db.session.execute(statement).scalars()

    return render_template("books.html", books=books)

@app.route("/users")
def users():
    statement = db.select(User)
    users = db.session.execute(statement).scalars()

    return render_template("users.html", users=users)

@app.route('/categories/')
@app.route("/categories/<string:name>")
def category_detail(name):
    statement = db.select(Book).where(Book.category.has(Category.name == name))
    books = db.session.execute(statement).scalars()

    # NOTE: why do i need this
    categorey_statement = db.select(Book).where(Book.category.has(Category.name == name))
    category = db.session.execute(categorey_statement).scalar()

    error = "CATEGORY NOT FOUND!"
    if not category:
        return render_template("base.html", text=error), 404
    return render_template("category_base.html", books=books)

@app.route("/categories")
def categories():
    statement = db.select(Category)
    categories = db.session.execute(statement).scalars()

    return render_template("categories.html", categories=categories)

@app.route('/books/')
@app.route('/books/<int:id>')
def book_id(id):
    statement = db.select(Book).where(Book.id == id)
    book = db.session.execute(statement).scalar()

    error = "BOOK NOT FOUND!"
    if not book:
        return render_template("base.html", text=error), 404
    return render_template("book_base.html", book=book)

@app.route('/user/')
@app.route('/user/<int:id>')
def user_id(id):
    statement = db.select(User).where(User.id == id)
    statement2 = db.select(BookRental).where(BookRental.user_id == id)
    user = db.session.execute(statement).scalar()
    user_rentals = db.session.execute(statement2).scalars()

    error = "USER NOT FOUND!"
    if not user:
        return render_template("base.html", text=error), 404
    return render_template("user.html", user=user, user_rentals=user_rentals)


@app.route('/available')
def available():
    statement = db.select(Book).where(~Book.rentals.any() | Book.rentals.any(BookRental.returned_on < datetime.now())).order_by(Book.title)
    books = db.session.execute(statement).scalars()

    return render_template("available.html", books=books)

@app.route('/rented')
def rented():
    book_ids_stmt = db.select(BookRental.book_id).where(BookRental.rented_on < datetime.now()).where(BookRental.returned_on == None)
    book_ids = [id for id in db.session.execute(book_ids_stmt).scalars()]
    ordered_books = db.select(Book).where(Book.id.in_(book_ids)).order_by(Book.title)
    books = db.session.execute(ordered_books).scalars()

    return render_template("rented.html", books=books)

if __name__ == "__main__":
    app.run(debug=True, port=8888)
    # with app.app_context():
    #     statement = db.select(Category)
    #     category = db.session.execute(statement).scalars()
    #     print(category)
    #
    #     for i in category:
    #         print(i.name)

```
### models.py
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
### manage.py
```
from db import db
from models import Category, Book, User, BookRental
from sqlalchemy import select
from sqlalchemy.sql import func
import csv
from app import app
from datetime import datetime, timedelta
from random import random, randint as rndm

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

def generate_rental_dates():
    now = datetime.now()
    # A book was rented sometime between 10 days ago and 24 days and 4 hours ago
    # Minutes and seconds stay the same
    random_past_offset = timedelta(days=rndm(10,25), hours=rndm(0,5))
    rented_on = now - random_past_offset
    # Decide whether the book was returned (50% chance)
    returned = random() > 0.5
    if not returned:
        returned_on = None
    else:
        returned_on = rented_on + timedelta(days=rndm(2, 9), hours=rndm(0,100), minutes=rndm(0,100))
    return rented_on, returned_on


def import_rentals(rented_on, returned_on):
    random_user = select(User).order_by(func.random())
    # FIX: this shit is broken
    # random_book = select(Book).order_by(func.random()).where(Book.rentals.any(BookRental.returned_on == None))
    random_book = select(Book).order_by(func.random()).where(~Book.rentals.any())
    user = db.session.execute(random_user).scalar()
    book = db.session.execute(random_book).scalar()
    print(book)

    br = BookRental(user=user, book_id=book.id, rented_on=rented_on, returned_on=returned_on)
    db.session.add(br)
    db.session.commit()

with app.app_context():
    create_db()
    import_books()
    import_users()
    # import_rentals(*generate_rental_dates()) 
    for _ in range(100):
        import_rentals(*generate_rental_dates()) 
```
### db.py
```
from flask_sqlalchemy import SQLAlchemy
from sqlalchemy.orm import DeclarativeBase

class Base(DeclarativeBase):
    pass

db = SQLAlchemy(model_class=Base)
```

### books.html
```
{% extends "base.html" %}

{% block content %}
<h1>Books</h1>
{% for book in books %}
<div>
    <div class="card">
        <div class="card-body">
            <h5 class="card-title">{{ book.title }}</h5>
            <p class="card-text">Price: £{{ book.price }}</p>
            <p class="card-text">Available: {{ book.available }}</p>
            <p class="card-text">Rating: {{ book.rating }}</p>
            <p class="card-text">UPC: {{ book.upc }}</p>
            <p class="card-text">URL: <a href="{{ book.url }}">{{ book.url }}</a></p>
            <p class="card-text">Category: {{ book.category.name }}</p>
            <a class="navbar-brand" href="{{ url_for('book_id', id=book.id) }}">Rental Records</a>
        </div>
    </div>
</div>
{% endfor %}
{% endblock %}

```