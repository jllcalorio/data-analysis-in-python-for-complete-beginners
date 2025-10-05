---
section: Intermediate Python
nav_order: 2
title: Importing Functions from Modules
topics: import, function, module
---

Python's power comes from its vast ecosystem of modules. Learning to import and use functions from modules effectively is crucial for productive programming.

{% include question.html header="Basic Import Statements" text="

Below are the common ways to import functions that are already built by other people, i.e., the developers of the functions.

**Import entire module**

```python
import math
result = math.sqrt(16)  # Use with module.function
print(result)  # 4.0
```

**Import specific functions**

```python
from math import sqrt, pi, ceil
result = sqrt(25)  # Use directly without module name
area = pi * 5**2
rounded_up = ceil(4.2)
```

**Import with alias**

```python
import math as m
result = m.factorial(5)

# Import specific function with alias
from math import factorial as fact
result = fact(5)
```
" %}

# Common Built-in Modules

## Math Module
```python
import math

# Basic mathematical operations
print(math.sqrt(16))      # Square root: 4.0
print(math.pow(2, 3))     # Power: 8.0
print(math.factorial(5))  # Factorial: 120

# Trigonometric functions
print(math.sin(math.pi/2))  # Sine: 1.0
print(math.cos(0))          # Cosine: 1.0

# Logarithms
print(math.log(10))         # Natural log
print(math.log10(100))      # Base-10 log: 2.0

# Rounding and ceiling
print(math.ceil(4.2))       # Round up: 5
print(math.floor(4.8))      # Round down: 4

# Constants
print(math.pi)              # 3.141592653589793
print(math.e)               # 2.718281828459045
```

## Random Module
```python
import random

# Generate random numbers
print(random.random())          # Float between 0-1
print(random.randint(1, 10))    # Integer between 1-10
print(random.uniform(1.5, 10.5))  # Float between 1.5-10.5

# Work with sequences
fruits = ["apple", "banana", "orange", "grape"]
print(random.choice(fruits))    # Random choice
print(random.sample(fruits, 2)) # Random sample of 2 items

# Shuffle a list
numbers = [1, 2, 3, 4, 5]
random.shuffle(numbers)
print(numbers)  # List is now shuffled

# Set seed for reproducible results
random.seed(42)
print(random.randint(1, 100))  # Will always be the same with seed 42
```

## Datetime Module
```python
from datetime import datetime, date, timedelta

# Current date and time
now = datetime.now()
today = date.today()

print(f"Current datetime: {now}")
print(f"Today's date: {today}")

# Formatting dates
formatted_date = now.strftime("%Y-%m-%d %H:%M:%S")
print(f"Formatted: {formatted_date}")

# Date arithmetic
tomorrow = today + timedelta(days=1)
next_week = today + timedelta(weeks=1)
past_date = today - timedelta(days=30)

print(f"Tomorrow: {tomorrow}")
print(f"Next week: {next_week}")
print(f"30 days ago: {past_date}")

# Parse date strings
date_string = "2025-12-25"
christmas = datetime.strptime(date_string, "%Y-%m-%d")
print(f"Christmas: {christmas}")
```

## OS Module
```python
import os

# Get current working directory
current_dir = os.getcwd()
print(f"Current directory: {current_dir}")

# List files in directory
files = os.listdir(".")
print(f"Files in current directory: {files}")

# Environment variables
user = os.getenv("USER", "Unknown")  # Get USER env var with default
print(f"Current user: {user}")

# Path operations
file_path = os.path.join("data", "files", "example.txt")
print(f"File path: {file_path}")

# Check if file/directory exists
print(f"Path exists: {os.path.exists(file_path)}")
```

## Creating Import-Friendly Functions
```python
# utils.py - A module you might create
def format_currency(amount, currency="USD"):
    """Format a number as currency."""
    return f"{currency} {amount:,.2f}"

def validate_email(email):
    """Basic email validation."""
    return "@" in email and "." in email.split("@")[1]

def calculate_tip(bill_amount, tip_percentage=15):
    """Calculate tip amount."""
    return bill_amount * (tip_percentage / 100)

# main.py - Using your module
from utils import format_currency, calculate_tip

bill = 85.50
tip = calculate_tip(bill, 18)
total = bill + tip

print(f"Bill: {format_currency(bill)}")
print(f"Tip: {format_currency(tip)}")
print(f"Total: {format_currency(total)}")
```
