QUIZ QUESTIONS START HERE

Select the pieces of code that will sort the list `my_list` in decreasing order, and keep the result in `my_list`:
my_list.sort(reverse=True)
my_list = sorted(my_list, reverse=True)

How do you add an element with key 'quiz' to an existing dictionary `my_var`?
`my_var.update(quiz=element)`

```
def my_function(arg1, arg2, arg3="quiz"):
  return "hello", "goodbye"
```
How many return values does the "my_function" have?
1, In Python, "hello", "goodbye" is the same as ("hello", "goodbye") - ONE tuple.

HANGMAN STARTS HERE

```
import random
import sys

class SecretWord:
    def __init__(self, word=None) -> None:
        if word == None:
            self.word = self.pick_random_word()
        else:
            self.word = word.upper()

    def pick_random_word(self):
        with open("words.txt", "r") as file:
            random_word_list = file.readlines()
            word_idx = random.randint(0, len(random_word_list))
            random_word = random_word_list[word_idx]
        return random_word.strip().upper()
    
    def show_letters(self, letters):
        return_string = []
        for character in self.word:
            if character.upper() in letters:
                return_string.append(character.upper())
            else:
                return_string.append("_")
        print(return_string)
        return " ".join(return_string)
    
    def check_letters(self, letters):
        revealed = self.show_letters(letters)
        if "_" in revealed:
            return False
        else:
            return True
        
    def check(self, word):
        if word.upper() == self.word:
            return True
        else:
            return False

class Game:
    def __init__(self, life=10, word=None) -> None:
        print(word)
        self.life = int(life)
        self.word = SecretWord(word)
        self.guesses = []

    def print_game(self):
        print("")
        print(self.word.show_letters(self.guesses))
        print(f"You have {self.life} turns left")
        
    def take_input(self):
        self.user_input = input("Guess a letter or word: ")
        print(self.user_input)
        if not self.user_input.isalpha():
            print("only 1 LETTER, noob")
        else:
            self.life -= 1
            return self.guesses.append(self.user_input.upper())
        
    def check_life(self):
        if self.life > 0:
            return False
        else:
            return True
        
    def start(self):
        while self.life > 0:
            self.print_game()
            self.take_input()
            if self.check_life():
                print("Game over.")
                break
            elif self.word.check(self.user_input) or self.word.check_letters(self.guesses):
                print("You win.")
                break
        
if __name__ == "__main__":
    Game(sys.argv[1], sys.argv[2]).start() if len(sys.argv) > 2 else Game().start()

```

HANGMAN TEST CASES STARTS HERE

```
from hangman2 import SecretWord

def test_secret_word_show_letters():
    word = SecretWord("vancouver")
    assert word.show_letters(["V"]) == "V _ _ _ _ _ V _ _"
    assert word.show_letters(["V", "A"]) == "V A _ _ _ _ V _ _"

def test_secret_word_check_letters():
    word = SecretWord("pizza")
    assert word.check_letters(["P", "I", "Z", "A"]) is True
    assert word.check_letters(["A", "Z", "P", "I"]) is True

    word = SecretWord("Tim")
    assert word.check_letters(["G"]) is False

def test_secret_word_check():
    word = SecretWord("vancouver")
    assert word.check("VanCOuver") is True
    assert word.check("VANCOUVER") is True
    assert word.check("hello") is False

```

RANDOM TEST CASE START HERE

```
def test_add_values():
	result = add_values(2,3)
	assert result == 5
```

RAISE ERROR EXAMPLE

```
def add_values(a, b):  
	if type(a) is not int or type(b) is not int:  
		raise TypeError("Invalid value")  
	return a+b
```

RANDOM SHIT STARTS HERE

py -m venv venv - must activate after this command use script in venv/Scripts folder

capitalize() Converts the first character to upper case
casefold() Converts string into lower case
center() Returns a centered string
count() Returns the number of times a specified value occurs in a string
encode() Returns an encoded version of the string
endswith() Returns true if the string ends with the specified value
expandtabs() Sets the tab size of the string
find() Searches the string for a specified value and returns the position of where it was found
format() Formats specified values in a string
format_map() Formats specified values in a string
index() Searches the string for a specified value and returns the position of where it was found
isalnum() Returns True if all characters in the string are alphanumeric
isalpha() Returns True if all characters in the string are in the alphabet
isascii() Returns True if all characters in the string are ascii characters
isdecimal() Returns True if all characters in the string are decimals
isdigit() Returns True if all characters in the string are digits
isidentifier() Returns True if the string is an identifier
islower() Returns True if all characters in the string are lower case
isnumeric() Returns True if all characters in the string are numeric
isprintable() Returns True if all characters in the string are printable
isspace() Returns True if all characters in the string are whitespaces
istitle() Returns True if the string follows the rules of a title
isupper() Returns True if all characters in the string are upper case
join() Converts the elements of an iterable into a string
ljust() Returns a left justified version of the string
lower() Converts a string into lower case
lstrip() Returns a left trim version of the string
maketrans() Returns a translation table to be used in translations
partition() Returns a tuple where the string is parted into three parts
replace() Returns a string where a specified value is replaced with a specified value
rfind() Searches the string for a specified value and returns the last position of where it was found
rindex() Searches the string for a specified value and returns the last position of where it was found
rjust() Returns a right justified version of the string
rpartition() Returns a tuple where the string is parted into three parts
rsplit() Splits the string at the specified separator, and returns a list
rstrip() Returns a right trim version of the string
split() Splits the string at the specified separator, and returns a list
splitlines() Splits the string at line breaks and returns a list
startswith() Returns true if the string starts with the specified value
strip() Returns a trimmed version of the string
swapcase() Swaps cases, lower case becomes upper case and vice versa
title() Converts the first character of each word to upper case
translate() Returns a translated string
upper() Converts a string into upper case
zfill() Fills the string with a specified number of 0 values at the beginning

LISTS

append() Adds an element at the end of the list
clear() Removes all the elements from the list
copy() Returns a copy of the list
count() Returns the number of elements with the specified value
extend() Add the elements of a list (or any iterable), to the end of the current list
index() Returns the index of the first element with the specified value
insert() Adds an element at the specified position
pop() Removes the element at the specified position
remove() Removes the first item with the specified value
reverse() Reverses the order of the list
sort() Sorts the list

DICTIONARIES

clear() Removes all the elements from the dictionary
copy() Returns a copy of the dictionary
fromkeys() Returns a dictionary with the specified keys and value
get() Returns the value of the specified key
items() Returns a list containing a tuple for each key value pair
keys() Returns a list containing the dictionary's keys
pop() Removes the element with the specified key
popitem() Removes the last inserted key-value pair
setdefault() Returns the value of the specified key. If the key does not exist: insert the key, with the specified value
update() Updates the dictionary with the specified key-value pairs
values() Returns a list of all the values in the dictionary

SET METHODS

add() Adds an element to the set
clear() Removes all the elements from the set
copy() Returns a copy of the set
pop() Removes an element from the set
remove() Removes the specified element

TUPLE METHODS  

count() Returns the number of times a specified value occurs in a tuple
index() Searches the tuple for a specified value and returns the position of where it was found  

x, y, z = "Orange", "Banana", "Cherry"  
x = y = z = "Orange"
fruits = ["apple", "banana", "cherry"]
x, y, z = fruits

Sequence[start:end:step]  
start: The index where the slice begins (inclusive).
end: The index where the slice ends (exclusive). It does not include the element at this index.
step (optional): The step or increment between each index in the slice.

min() return smallest number
max() return biggest number
sum() sum

full_name = f”{first_name} {last_name}”

.sort() sort and change original list
sorted() sort list temporarily

copy_of_bikes = bikes[:] copy a list

Test files start with test_* or \*\_test
Test functions/methods start with test_
Tests can be methods inside classes only if class start with Test

SCRAPING STARTS HERE

book.py
```
import httpx
from bs4 import BeautifulSoup
import re

RATINGS = {"one": 1, "two": 2, "three": 3, "four": 4, "five": 5}

class Book:
    def __init__(self, url):
        response = httpx.get(url)
        soup = BeautifulSoup(response.text, "html.parser")

        self.url = url

        self.title = soup.find("h1")
        if self.title == None:
            raise RuntimeError("Parsing error with title")
        else:
            self.title = self.title.text

        self.price = soup.select(".product_main p.price_color")
        if len(self.price) > 0:
            self.price = float(self.price[0].text[1:])
        else:
            raise RuntimeError("Parsing error with price")

        self.upc = soup.find("th", string="UPC").next_sibling.text
        if not self.upc:
            raise RuntimeError("Parsing error with upc")

        rating = soup.find("p", attrs={"class": "star-rating"}).attrs["class"]
        rating.remove("star-rating")
        if rating == None:
            raise RuntimeError("Parsing error with rating")
        else:
            for key in RATINGS.keys():
                if rating[0].lower() == key:
                    self.rating = RATINGS[key]

        stock_text = soup.select(".product_main p.availability")[0].text
        pattern = r"In stock \((\d+) available\)"
        matches = re.search(pattern, stock_text)
        self.available = int(matches.group(1))

    def to_dict(self):
        return {
            "title": self.title,
            "price": self.price,
            "available": self.available,
            # "URL": self.url,
            "rating": self.rating,
            "upc": self.upc,
        }
```

my scraper.py 
```
from book import Book
import httpx
from bs4 import BeautifulSoup
import csv
from urllib.parse import urljoin

BASE_URL = "https://books.toscrape.com/index.html"

response = httpx.get(BASE_URL)
soup = BeautifulSoup(response.text, "html.parser")

def scrape():
    book_objects = []
    href_book = soup.select(".product_pod h3 a")
    href_next = soup.select("li.next a")
    print(href_next)
    for i in href_book:
        book_url = urljoin(BASE_URL, i.attrs["href"])
        book_objects.append(Book(book_url))

    return book_objects

scraped = scrape()
```

tim's scraper.py
```

import csv
from urllib.parse import urljoin

import httpx
from bs4 import BeautifulSoup

from book import Book

def scrape(url="https://books.toscrape.com/index.html"):
    # An array with all the book objects
    books = []

    # The CSV file we write to
    out = open("books.csv", "w", newline="")
    writer = csv.DictWriter(out, fieldnames=Book.FIELDS)
    writer.writeheader()

    keep_going = True
    while keep_going:
        # Main loop
        print("--- INDEX PAGE ---", url)
        
        response = httpx.get(url)
        
        soup = BeautifulSoup(response.text, "html.parser")
        # Find book links and create book objects
        for book in soup.select(".product_pod h3 a"):            
            book_url = urljoin(url, book.attrs["href"])
            book_obj = Book(book_url)
            # Add the book object to the list
            books.append(book_obj)
            # Write to the CSV file
            writer.writerow(book_obj.to_dict())
            
        # Find the next page link
        next_link = soup.select("li.next a")
        
        if not next_link or len(next_link) == 0:
            # No link found - we stop the loop
            keep_going = False
        else:
            # Update the URL and do it again
            url = urljoin(url, next_link[0].attrs["href"])
    
    out.close()
    return books


if __name__ == "__main__":
    books = scrape()
```

test_scraper_all.py
```
from unittest.mock import patch, Mock
from book import Book
from scraper import scrape

with open("test_book_1.html") as fp:
    BOOK_1 = fp.read()

with open("test_index.html") as fp:
    INDEX_PAGE = fp.read()
    
with open("test_page_2.html") as fp:
    INDEX_PAGE_2 = fp.read()
    
with open("test_index_last.html") as fp:
    INDEX_LAST_PAGE = fp.read()

class FakeResponseBook:
    status_code = 200
    text = BOOK_1

class FakeResponseIndex:
    status_code = 200
    text = INDEX_PAGE

class FakeResponseIndexPage2:
    status_code = 200
    text = INDEX_PAGE_2
    
class FakeResponseIndexLast:
    status_code = 200
    text = INDEX_LAST_PAGE

def side_effect():
    # Tweaking the generator: the first response will be the index page, then there will be 19 book pages
    # (there are 19 book links on the index page)
    # and then the index page again (supposed to be page 2), with 19 book pages, etc.
    # The last page does not have a "next" link.
    # There will be 5 index pages in total = 95 books.

    for counter in range(1, 6):
        if counter == 1:
            yield FakeResponseIndex()
        elif counter == 5:
            yield FakeResponseIndexLast()
        else:
            yield FakeResponseIndexPage2()

        for _ in range(19):
            yield FakeResponseBook()

@patch('scraper.httpx.get', side_effect=side_effect())
def test_scrape(mock_get):
    books = scrape()
    assert len(books) == 95
    assert all([type(b) is Book for b in books])
    assert books[0].title == "The Requiem Red"
    assert books[0].url == "https://books.toscrape.com/catalogue/a-light-in-the-attic_1000/index.html"
    assert books[10].upc == "ACIT2515"
    assert books[10].url == "https://books.toscrape.com/catalogue/starving-hearts-triangular-trade-trilogy-1_990/index.html"
    assert books[-1].url == "https://books.toscrape.com/catalogue/libertarianism-for-beginners_982/index.html"

```

test_scraper_index.py
```
import pytest
from unittest.mock import patch, Mock
from book import Book
from scraper import scrape

with open("test_book_1.html") as fp:
    BOOK_1 = fp.read()

with open("test_index.html") as fp:
    INDEX_PAGE = fp.read()

class FakeResponseBook:
    status_code = 200
    text = BOOK_1
      
    def get(self, *args, **kwargs):
        print(args, kwargs)
        return Mock()

class FakeResponseIndex:
    status_code = 200
    text = INDEX_PAGE

def side_effect():
    # This is a "generator".
    # When called, this function returns a special object that can be iterated over.
    # In our case, we want the first response to be the index page, and the rest to be book pages.
    # All boook pages will be the same, but it is just for demonstration purposes.
    yield FakeResponseIndex()
    while True:
        yield FakeResponseBook()

@patch('scraper.httpx.get', side_effect=side_effect())
def test_scrape(mock_get):
    books = scrape()
    assert len(books) == 19
    assert all([type(b) is Book for b in books])
    assert books[0].title == "The Requiem Red"
    assert books[0].url == "https://books.toscrape.com/catalogue/a-light-in-the-attic_1000/index.html"
    assert books[10].upc == "ACIT2515"
    assert books[10].url == "https://books.toscrape.com/catalogue/starving-hearts-triangular-trade-trilogy-1_990/index.html"
```

test_hangman.py
```
import pytest
from unittest.mock import patch, mock_open
from hangman import Game


@pytest.fixture
@patch("builtins.open", new_callable=mock_open, read_data="aaaaa")
def game_word_is_a(mock_file):
    """Game object, 5 turns, word is aaaaa"""

    return Game(5)


@pytest.fixture
@patch("builtins.open", new_callable=mock_open, read_data="testword")
def game_word_is_testword(mock_file):
    """Game object, 10 turns, word is testword"""

    return Game(10)


def test_turns(game_word_is_a):
    # Default value is 10
    with patch("builtins.open", new_callable=mock_open, read_data="whatever"):
        assert Game().turns == 10

    # This particular game has 5 (see fixture)
    assert game_word_is_a.turns == 5


def test_play_one_round_a(game_word_is_a):
    with patch("builtins.input", return_value="a") as mock_input:
        assert game_word_is_a.play_one_round() is True
        assert game_word_is_a.turns == 4


def test_play_one_round_a_empty_input(game_word_is_a):
    with patch(
        "builtins.input", side_effect=["", "", "", "", "", "", "a", "b"]
    ) as mock_input:
        assert game_word_is_a.play_one_round() is True
        # play_one_round returns as soon as ONE valid guess is provided
        assert game_word_is_a.turns == 4


def test_play_one_round_aa(game_word_is_a):
    with patch("builtins.input", return_value="aa"):
        # Wrong guess - the word is not 'aa'
        assert game_word_is_a.play_one_round() is False
        # It still took one turn
        assert game_word_is_a.turns == 4


def test_play_one_round_check(game_word_is_testword):
    # Check lower/uppercase
    with patch("builtins.input", return_value="TESTWORD"):
        assert game_word_is_testword.play_one_round() is True


def test_play_game_a(game_word_is_a):
    with patch(
        "builtins.input", side_effect=["", "", "", "", "", "", "b", "a"]
    ) as mock_input:
        assert game_word_is_a.play() is True
        # Took 2 turns to find the word ('b', then 'a')
        assert game_word_is_a.turns == 3


def test_play_game_testword_win(game_word_is_testword):
    with patch(
        "builtins.input",
        side_effect=["t", "T", "E", "s", "w", "o", "r", "a", "b", "c", "d"],
    ) as mock_input:
        assert game_word_is_testword.play() is True
        # t = T, case does not matter = 10 turns required
        assert game_word_is_testword.turns == 0


def test_play_game_testword_win_goated(game_word_is_testword):
    with patch("builtins.input", side_effect=["dunno", "testWORd"]) as mock_input:
        assert game_word_is_testword.play() is True
        # Takes two turns to guess the full word
        assert game_word_is_testword.turns == 8
        

def test_play_game_testword_lose(game_word_is_testword):
    with patch(
        "builtins.input", side_effect=["a", "b", "c", "d", "e", "f", "g", "t", "s", "w"]
    ) as mock_input:
        assert game_word_is_testword.play() is False
        assert game_word_is_testword.turns == 0

```