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