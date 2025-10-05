---
section: Intermediate Python
nav_order: 4
title: Modules
topics: Template; Basic Config
---

Understanding **modules** is key to organizing your code and leveraging Python's ecosystem effectively.

## What Are Modules?

A module is simply a Python file containing functions, classes, and variables. Any .py file can be imported as a module.

{% include question.html header="Creating Your Own Modules" text="

Example: calculator.py

```python
# A simple calculator module.
# This module provides basic mathematical operations.

def add(a, b):
    """Add two numbers."""
    return a + b

def subtract(a, b):
    """Subtract second number from first."""
    return a - b

def multiply(a, b):
    """Multiply two numbers."""
    return a * b

def divide(a, b):
    """Divide first number by second."""
    if b == 0:
        raise ValueError("Cannot divide by zero!")
    return a / b

def power(base, exponent):
    """Raise base to the power of exponent."""
    return base ** exponent

# Module-level variables
PI = 3.14159
E = 2.71828

# Code that runs when module is imported
print(f"Calculator module loaded. PI = {PI}")

# Code that only runs when module is executed directly
if __name__ == "__main__":
    print("Running calculator module tests...")
    print(f"5 + 3 = {add(5, 3)}")
    print(f"10 - 4 = {subtract(10, 4)}")
    print(f"6 * 7 = {multiply(6, 7)}")
    print(f"15 / 3 = {divide(15, 3)}")
```
" %}

## Using Your Module
```python
# main.py
import calculator

# Use functions from the module
result1 = calculator.add(10, 5)
result2 = calculator.multiply(4, 7)

print(f"Addition result: {result1}")
print(f"Multiplication result: {result2}")
print(f"PI value: {calculator.PI}")

# Alternative import methods
from calculator import add, subtract, PI
result3 = add(20, 15)
result4 = subtract(30, 12)

# Import with alias
import calculator as calc
result5 = calc.power(2, 8)
```

# Module Organization Best Practices

## Creating a Package

```my_project/
    __init__.py          # Makes it a package
    math_utils/
        __init__.py      # Makes it a subpackage
        basic.py         # Basic math functions
        advanced.py      # Advanced math functions
    string_utils/
        __init__.py
        formatters.py    # String formatting functions
        validators.py    # String validation functions
    main.py
```

## math_utils/basic.py

```python
"""Basic mathematical operations."""

def add_list(numbers):
    """Add all numbers in a list."""
    return sum(numbers)

def average(numbers):
    """Calculate average of a list of numbers."""
    if not numbers:
        return 0
    return sum(numbers) / len(numbers)

def find_max_min(numbers):
    """Find maximum and minimum values."""
    if not numbers:
        return None, None
    return max(numbers), min(numbers)
```

## math_utils/init.py

```python
"""Math utilities package."""

from .basic import add_list, average, find_max_min
from .advanced import fibonacci, is_prime

__version__ = "1.0.0"
__author__ = "Your Name"

# Package-level function
def package_info():
    return f"Math Utils v{__version__} by {__author__}"
```

## Using the Package

```python
# Import from package
from math_utils import add_list, average
from math_utils.advanced import fibonacci

# Use the functions
numbers = [1, 2, 3, 4, 5]
total = add_list(numbers)
avg = average(numbers)
fib_sequence = fibonacci(10)

print(f"Sum: {total}, Average: {avg}")
print(f"Fibonacci: {fib_sequence}")
```
