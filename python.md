# Python Cheat Sheet

Quick reference for Python 3.x syntax, built-in features, and common patterns. Examples focus on practical, everyday programming tasks.

## Table of Contents

- [Basics](#basics)
- [Data Types](#data-types)
- [Operators](#operators)
- [Control Flow](#control-flow)
- [Functions](#functions)
- [Data Structures](#data-structures)
- [Comprehensions](#comprehensions)
- [String Operations](#string-operations)
- [File I/O](#file-io)
- [Error Handling](#error-handling)
- [Classes and Objects](#classes-and-objects)
- [Modules and Packages](#modules-and-packages)
- [Virtual Environments](#virtual-environments)
- [Common Libraries](#common-libraries)
- [Decorators](#decorators)
- [Generators and Iterators](#generators-and-iterators)
- [Context Managers](#context-managers)
- [Type Hints](#type-hints)
- [Best Practices](#best-practices)
- [Troubleshooting](#troubleshooting)
- [Tools & References](#tools--references)

## Basics

```python
# Comments start with #
"""
Multi-line strings can serve as
multi-line comments (though technically they're string literals)
"""

# Print to console
print("Hello, World!")
print(f"Formatted: {42}")  # f-strings (Python 3.6+)

# Variables (no declaration needed)
x = 10
name = "Alice"
is_valid = True

# Multiple assignment
a, b, c = 1, 2, 3
x = y = z = 0

# Type checking
type(42)        # <class 'int'>
isinstance(42, int)  # True
```

## Data Types

```python
# Numeric types
integer = 42
floating = 3.14
complex_num = 3 + 4j

# Strings
text = "Hello"
multiline = """Line 1
Line 2"""
raw_string = r"C:\path\no\escape"  # raw string

# Boolean
is_true = True
is_false = False

# None (null equivalent)
nothing = None

# Type conversion
int("42")       # 42
float("3.14")   # 3.14
str(42)         # "42"
bool(1)         # True
bool(0)         # False
```

## Operators

```python
# Arithmetic
+ - * / // % **  # add, subtract, multiply, divide, floor divide, modulo, power

# Comparison
== != < > <= >=

# Logical
and or not

# Membership
'a' in 'abc'     # True
'x' not in [1, 2, 3]  # True

# Identity
x is y           # same object
x is not y

# Bitwise
& | ^ ~ << >>

# Assignment operators
+= -= *= /= //= %= **=

# Walrus operator (Python 3.8+)
if (n := len(items)) > 10:
    print(f"List has {n} items")
```

## Control Flow

```python
# if/elif/else
if x > 0:
    print("positive")
elif x < 0:
    print("negative")
else:
    print("zero")

# Ternary operator
result = "even" if x % 2 == 0 else "odd"

# while loop
i = 0
while i < 5:
    print(i)
    i += 1

# for loop
for i in range(5):         # 0, 1, 2, 3, 4
    print(i)

for i in range(2, 10, 2):  # start, stop, step
    print(i)               # 2, 4, 6, 8

# Iterate over collections
for item in [1, 2, 3]:
    print(item)

for key, value in {"a": 1, "b": 2}.items():
    print(f"{key}: {value}")

# break, continue, else
for i in range(10):
    if i == 3:
        continue  # skip to next iteration
    if i == 7:
        break     # exit loop
else:
    print("Loop completed normally")  # only runs if no break

# match/case (Python 3.10+)
match status:
    case 200:
        print("OK")
    case 404:
        print("Not Found")
    case _:
        print("Other")
```

## Functions

```python
# Basic function
def greet(name):
    return f"Hello, {name}!"

# Default arguments
def greet(name="World"):
    return f"Hello, {name}!"

# Keyword arguments
def describe(name, age, city="Unknown"):
    return f"{name}, {age}, from {city}"

describe(name="Alice", age=30)
describe("Bob", 25, city="NYC")

# Variable arguments
def sum_all(*args):
    return sum(args)

sum_all(1, 2, 3, 4)  # 10

# Keyword variable arguments
def print_info(**kwargs):
    for key, value in kwargs.items():
        print(f"{key}: {value}")

print_info(name="Alice", age=30)

# Lambda (anonymous functions)
square = lambda x: x ** 2
add = lambda x, y: x + y

# Map, filter, reduce
list(map(lambda x: x * 2, [1, 2, 3]))  # [2, 4, 6]
list(filter(lambda x: x % 2 == 0, [1, 2, 3, 4]))  # [2, 4]

from functools import reduce
reduce(lambda x, y: x + y, [1, 2, 3, 4])  # 10
```

## Data Structures

```python
# Lists (mutable, ordered)
numbers = [1, 2, 3, 4, 5]
numbers.append(6)
numbers.insert(0, 0)
numbers.remove(3)
numbers.pop()          # remove and return last
numbers[0] = 10        # modify
len(numbers)
numbers.sort()         # in-place
sorted(numbers)        # returns new list

# Slicing
numbers[1:4]           # indices 1-3
numbers[:3]            # first 3
numbers[3:]            # from index 3
numbers[-2:]           # last 2
numbers[::2]           # every 2nd element
numbers[::-1]          # reverse

# Tuples (immutable, ordered)
coords = (10, 20)
x, y = coords          # unpacking

# Dictionaries (mutable, key-value)
person = {"name": "Alice", "age": 30}
person["city"] = "NYC"
person.get("age")
person.get("country", "Unknown")  # default
person.keys()
person.values()
person.items()
del person["age"]
person.pop("city")

# Sets (mutable, unordered, unique)
nums = {1, 2, 3, 3}    # {1, 2, 3}
nums.add(4)
nums.remove(2)
nums.discard(10)       # no error if missing

# Set operations
a = {1, 2, 3}
b = {3, 4, 5}
a | b                  # union: {1, 2, 3, 4, 5}
a & b                  # intersection: {3}
a - b                  # difference: {1, 2}
a ^ b                  # symmetric difference: {1, 2, 4, 5}
```

## Comprehensions

```python
# List comprehension
squares = [x**2 for x in range(10)]
evens = [x for x in range(20) if x % 2 == 0]

# Dict comprehension
square_dict = {x: x**2 for x in range(5)}

# Set comprehension
unique_lengths = {len(word) for word in ["hello", "world", "hi"]}

# Generator expression (memory efficient)
squares_gen = (x**2 for x in range(1000000))

# Nested comprehension
matrix = [[i*j for j in range(3)] for i in range(3)]
flattened = [item for row in matrix for item in row]
```

## String Operations

```python
# Methods
s = "  Hello, World!  "
s.lower()              # "  hello, world!  "
s.upper()              # "  HELLO, WORLD!  "
s.strip()              # "Hello, World!"
s.replace("World", "Python")
s.split(",")           # ["  Hello", " World!  "]
"-".join(["a", "b", "c"])  # "a-b-c"
s.startswith("Hello")
s.endswith("!")
s.find("World")        # index or -1
s.count("l")

# Formatting
name = "Alice"
age = 30

# f-strings (preferred, Python 3.6+)
f"Name: {name}, Age: {age}"
f"{age:.2f}"           # format numbers

# format method
"Name: {}, Age: {}".format(name, age)
"Name: {n}, Age: {a}".format(n=name, a=age)

# Old style (avoid)
"Name: %s, Age: %d" % (name, age)

# Multi-line strings
text = """Line 1
Line 2
Line 3"""
```

## File I/O

```python
# Read entire file
with open("file.txt", "r") as f:
    content = f.read()

# Read lines
with open("file.txt", "r") as f:
    lines = f.readlines()  # list of lines

# Read line by line (memory efficient)
with open("file.txt", "r") as f:
    for line in f:
        print(line.strip())

# Write to file
with open("output.txt", "w") as f:
    f.write("Hello\n")
    f.writelines(["Line 1\n", "Line 2\n"])

# Append to file
with open("output.txt", "a") as f:
    f.write("Appended line\n")

# Read/write JSON
import json

# Write JSON
data = {"name": "Alice", "age": 30}
with open("data.json", "w") as f:
    json.dump(data, f, indent=2)

# Read JSON
with open("data.json", "r") as f:
    data = json.load(f)

# CSV files
import csv

# Read CSV
with open("data.csv", "r") as f:
    reader = csv.reader(f)
    for row in reader:
        print(row)

# Write CSV
with open("output.csv", "w", newline="") as f:
    writer = csv.writer(f)
    writer.writerow(["Name", "Age"])
    writer.writerow(["Alice", 30])

# CSV with dictionaries
with open("data.csv", "r") as f:
    reader = csv.DictReader(f)
    for row in reader:
        print(row["Name"])
```

## Error Handling

```python
# Basic try/except
try:
    result = 10 / 0
except ZeroDivisionError:
    print("Cannot divide by zero")

# Multiple exceptions
try:
    # risky code
    pass
except (ValueError, TypeError) as e:
    print(f"Error: {e}")

# Catch all (use sparingly)
try:
    # code
    pass
except Exception as e:
    print(f"Unexpected error: {e}")

# else and finally
try:
    result = int("42")
except ValueError:
    print("Invalid number")
else:
    print("Success!")  # runs if no exception
finally:
    print("Always runs")  # cleanup code

# Raising exceptions
def validate_age(age):
    if age < 0:
        raise ValueError("Age cannot be negative")
    return age

# Custom exceptions
class CustomError(Exception):
    pass

raise CustomError("Something went wrong")
```

## Classes and Objects

```python
# Basic class
class Person:
    def __init__(self, name, age):
        self.name = name
        self.age = age

    def greet(self):
        return f"Hello, I'm {self.name}"

    def __str__(self):
        return f"Person({self.name}, {self.age})"

person = Person("Alice", 30)
print(person.greet())

# Class variables vs instance variables
class Counter:
    count = 0  # class variable

    def __init__(self):
        Counter.count += 1
        self.id = Counter.count  # instance variable

# Properties
class Circle:
    def __init__(self, radius):
        self._radius = radius

    @property
    def radius(self):
        return self._radius

    @radius.setter
    def radius(self, value):
        if value < 0:
            raise ValueError("Radius must be positive")
        self._radius = value

    @property
    def area(self):
        return 3.14159 * self._radius ** 2

# Inheritance
class Student(Person):
    def __init__(self, name, age, student_id):
        super().__init__(name, age)
        self.student_id = student_id

    def study(self):
        return f"{self.name} is studying"

# Multiple inheritance
class A:
    def method(self):
        return "A"

class B:
    def method(self):
        return "B"

class C(A, B):  # Method Resolution Order: C -> A -> B
    pass

# Static and class methods
class MathUtils:
    @staticmethod
    def add(x, y):
        return x + y

    @classmethod
    def from_string(cls, string):
        # Factory method
        return cls()

# Dataclasses (Python 3.7+)
from dataclasses import dataclass

@dataclass
class Point:
    x: float
    y: float

    def distance(self):
        return (self.x**2 + self.y**2)**0.5
```

## Modules and Packages

```python
# Import entire module
import math
math.sqrt(16)

# Import specific items
from math import sqrt, pi
sqrt(16)

# Import with alias
import numpy as np
from datetime import datetime as dt

# Import all (avoid in production)
from math import *

# Create your own module
# file: mymodule.py
def my_function():
    return "Hello"

# file: main.py
import mymodule
mymodule.my_function()

# Package structure
"""
mypackage/
    __init__.py
    module1.py
    module2.py
    subpackage/
        __init__.py
        module3.py
"""

# Usage
from mypackage import module1
from mypackage.subpackage import module3

# __name__ check
if __name__ == "__main__":
    # Code here runs only when script is executed directly
    main()
```

## Virtual Environments

```bash
# Create virtual environment
python -m venv venv

# Activate (Windows)
venv\Scripts\activate

# Activate (Unix/macOS)
source venv/bin/activate

# Deactivate
deactivate

# Install packages
pip install requests
pip install -r requirements.txt

# Save dependencies
pip freeze > requirements.txt

# Upgrade pip
python -m pip install --upgrade pip
```

## Common Libraries

```python
# datetime
from datetime import datetime, timedelta

now = datetime.now()
today = datetime.today()
formatted = now.strftime("%Y-%m-%d %H:%M:%S")
parsed = datetime.strptime("2024-01-01", "%Y-%m-%d")
tomorrow = now + timedelta(days=1)

# os and pathlib
import os
from pathlib import Path

os.getcwd()                    # current directory
os.listdir(".")               # list directory
os.path.exists("file.txt")
os.path.join("dir", "file.txt")

# pathlib (modern, preferred)
path = Path("data/file.txt")
path.exists()
path.read_text()
path.write_text("content")
path.parent
path.stem                     # filename without extension
path.suffix                   # extension

# requests (HTTP library)
import requests

response = requests.get("https://api.example.com/data")
response.status_code
response.json()
response.text

response = requests.post("https://api.example.com/data",
                        json={"key": "value"},
                        headers={"Authorization": "Bearer token"})

# collections
from collections import Counter, defaultdict, deque

# Counter
words = ["apple", "banana", "apple", "cherry"]
count = Counter(words)        # Counter({'apple': 2, 'banana': 1, 'cherry': 1})
count.most_common(2)

# defaultdict
dd = defaultdict(list)
dd["key"].append("value")     # no KeyError

# deque (double-ended queue)
dq = deque([1, 2, 3])
dq.append(4)
dq.appendleft(0)
dq.pop()
dq.popleft()

# itertools
from itertools import chain, combinations, permutations, product

list(chain([1, 2], [3, 4]))   # [1, 2, 3, 4]
list(combinations([1, 2, 3], 2))  # [(1, 2), (1, 3), (2, 3)]
list(product([1, 2], ['a', 'b']))  # [(1, 'a'), (1, 'b'), (2, 'a'), (2, 'b')]

# random
import random

random.random()               # float [0.0, 1.0)
random.randint(1, 10)         # integer [1, 10]
random.choice([1, 2, 3])
random.shuffle(items)         # in-place
random.sample([1, 2, 3, 4], 2)  # 2 unique random items
```

## Decorators

```python
# Basic decorator
def my_decorator(func):
    def wrapper(*args, **kwargs):
        print("Before function")
        result = func(*args, **kwargs)
        print("After function")
        return result
    return wrapper

@my_decorator
def say_hello():
    print("Hello!")

# Decorator with arguments
def repeat(times):
    def decorator(func):
        def wrapper(*args, **kwargs):
            for _ in range(times):
                result = func(*args, **kwargs)
            return result
        return wrapper
    return decorator

@repeat(3)
def greet(name):
    print(f"Hello, {name}!")

# Common built-in decorators
class MyClass:
    @staticmethod
    def static_method():
        pass

    @classmethod
    def class_method(cls):
        pass

    @property
    def my_property(self):
        return self._value

# functools.wraps (preserves metadata)
from functools import wraps

def my_decorator(func):
    @wraps(func)
    def wrapper(*args, **kwargs):
        return func(*args, **kwargs)
    return wrapper
```

## Generators and Iterators

```python
# Generator function
def count_up_to(n):
    i = 1
    while i <= n:
        yield i
        i += 1

for num in count_up_to(5):
    print(num)

# Generator expression
squares = (x**2 for x in range(10))

# Iterator protocol
class Counter:
    def __init__(self, max_count):
        self.max_count = max_count
        self.count = 0

    def __iter__(self):
        return self

    def __next__(self):
        if self.count >= self.max_count:
            raise StopIteration
        self.count += 1
        return self.count

# itertools for advanced iteration
from itertools import islice, cycle, repeat

list(islice(range(100), 5))   # first 5 elements
```

## Context Managers

```python
# with statement (context manager)
with open("file.txt", "r") as f:
    content = f.read()
# file automatically closed

# Custom context manager (class-based)
class MyContext:
    def __enter__(self):
        print("Entering context")
        return self

    def __exit__(self, exc_type, exc_value, traceback):
        print("Exiting context")
        return False  # propagate exceptions

with MyContext() as ctx:
    print("Inside context")

# Context manager (function-based)
from contextlib import contextmanager

@contextmanager
def my_context():
    print("Setup")
    try:
        yield
    finally:
        print("Cleanup")

with my_context():
    print("Inside")
```

## Type Hints

```python
# Basic type hints (Python 3.5+)
def greet(name: str) -> str:
    return f"Hello, {name}!"

# Variable annotations (Python 3.6+)
age: int = 30
names: list[str] = ["Alice", "Bob"]

# Optional and Union
from typing import Optional, Union

def process(value: Optional[int] = None) -> str:
    return str(value) if value else "None"

def handle(x: Union[int, str]) -> str:
    return str(x)

# Generics
from typing import List, Dict, Tuple, Set

def process_items(items: List[int]) -> Dict[str, int]:
    return {"count": len(items)}

# Callable
from typing import Callable

def apply(func: Callable[[int, int], int], x: int, y: int) -> int:
    return func(x, y)

# Type aliases
Vector = List[float]

def scale(scalar: float, vector: Vector) -> Vector:
    return [scalar * num for num in vector]

# Any (escape hatch)
from typing import Any

def process(data: Any) -> Any:
    return data
```

## Best Practices

- Use meaningful variable and function names
- Follow PEP 8 style guide (use tools like `black`, `flake8`)
- Write docstrings for functions, classes, and modules
- Use list comprehensions for simple transformations
- Prefer `with` statements for resource management
- Use `enumerate()` instead of manual counters
- Use `zip()` to iterate over multiple sequences
- Avoid mutable default arguments
- Use virtual environments for project isolation
- Keep functions small and focused (single responsibility)
- Use type hints for better code documentation

```python
# Good practices examples

# enumerate instead of range(len())
for i, item in enumerate(items):
    print(f"{i}: {item}")

# zip for parallel iteration
names = ["Alice", "Bob"]
ages = [30, 25]
for name, age in zip(names, ages):
    print(f"{name}: {age}")

# Avoid mutable defaults
def add_item(item, items=None):  # Good
    if items is None:
        items = []
    items.append(item)
    return items

# Don't do this:
# def add_item(item, items=[]):  # Bad!
#     items.append(item)
#     return items

# Use get() with dict
value = my_dict.get("key", "default")

# String checking
if text:  # better than if text != ""
    pass

# List checking
if items:  # better than if len(items) > 0
    pass
```

## Troubleshooting

- **IndentationError**: Check consistent use of spaces (4 spaces recommended) or tabs
- **NameError**: Variable not defined or misspelled
- **TypeError**: Operation on incompatible types; check your data types
- **KeyError**: Dictionary key doesn't exist; use `.get()` with default
- **IndexError**: List index out of range; check list length
- **AttributeError**: Object doesn't have the attribute/method
- **ImportError/ModuleNotFoundError**: Module not installed or wrong import path
- **SyntaxError**: Check for missing colons, parentheses, or quotes
- **UnboundLocalError**: Assigning to variable before reading it in local scope

```python
# Common fixes

# Check if key exists
if "key" in my_dict:
    value = my_dict["key"]
# or
value = my_dict.get("key", default_value)

# Safe list access
if 0 <= index < len(my_list):
    item = my_list[index]

# Check None before using
if value is not None:
    value.method()

# Use debugger
import pdb; pdb.set_trace()  # breakpoint
# or (Python 3.7+)
breakpoint()
```

## Tools & References

- **Official Docs**: https://docs.python.org/3/
- **PEP 8**: Python style guide
- **PyPI**: Package index at https://pypi.org/
- **Real Python**: Tutorials and articles
- **Python Tutor**: Visualize code execution
- **mypy**: Static type checker
- **black**: Code formatter
- **pylint/flake8**: Linters
- **pytest**: Testing framework

---

Quick tip: Use `dir(obj)` to see available attributes/methods on any object, and `help(obj)` for documentation.
