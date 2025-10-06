---
section: Intermediate Python
nav_order: 4
title: Modules
topics: Template; Basic Config
---

Understanding **modules** is key to organizing your code and leveraging Python's ecosystem effectively.

## What Are Modules?

A module is simply a Python file containing functions, classes, and variables. Any ```.py``` file can be imported as a module.

{% include question.html header="Creating Your Own Modules" text="

**Example:** ```calculator.py```

- This is a simple calculator module.
- This module provides basic mathematical operations.

Let's define some functions:

```python
def add(a, b):
    \"\"\"Add two numbers.\"\"\"
    return a + b

def subtract(a, b):
    \"\"\"Subtract second number from first.\"\"\"
    return a - b

def multiply(a, b):
    \"\"\"Multiply two numbers.\"\"\"
    return a * b

def divide(a, b):
    \"\"\"Divide first number by second.\"\"\"
    if b == 0:
        raise ValueError(\"Cannot divide by zero!\")
    return a / b

def power(base, exponent):
    \"\"\"Raise base to the power of exponent.\"\"\"
    return base ** exponent
```

Let's also define module-level variables

```python
PI = 3.14159
E = 2.71828
```

Code that runs when module is imported

```python
print(f\"Calculator module loaded. PI = {PI}\")
```

Code that only runs when module is executed directly

```python
if __name__ == \"__main__\":
    print(\"Running calculator module tests...\")
    print(f\"5 + 3 = {add(5, 3)}\")
    print(f\"10 - 4 = {subtract(10, 4)}\")
    print(f\"6 * 7 = {multiply(6, 7)}\")
    print(f\"15 / 3 = {divide(15, 3)}\")
```
" %}

{% include question.html header="Using Your Module" text="
```python
# main.py
import calculator
```

Use functions from the module

```python
result1 = calculator.add(10, 5)
result2 = calculator.multiply(4, 7)

print(f\"Addition result: {result1}\")
print(f\"Multiplication result: {result2}\")
print(f\"PI value: {calculator.PI}\")
```

Alternative import methods

```python
from calculator import add, subtract, PI

result3 = add(20, 15)
result4 = subtract(30, 12)

print(result3)
print(result4)
```

Import with alias

```python
import calculator as calc

result5 = calc.power(2, 8)

print(result5)
```
" %}
