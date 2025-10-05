---
section: Beginning Python
nav_order: 5
title: Operators
topics: arithmetic, comparison, logical, assignment, operators
---

Operators allow you to perform operations on variables and values.

This includes mathematical operators, comparative operators, etc.

{% include question.html header="Arithmetic Operators"

Performing mathematical operators can be done in Python. If you remember PEMDAS, yes, it can be done.

Remember that PEMDAS is?
" solution="
PEMDAS is a mathematical acronym for the order of operations, namely
- Parentheses,
- Exponents,
- Multiplication,
- Division,
- Addition, and
- Subtraction.

" text="

```python
a = 10
b = 3

print(a + b)   # Addition: 13
print(a - b)   # Subtraction: 7
print(a * b)   # Multiplication: 30
print(a / b)   # Division: 3.333...
print(a // b)  # Floor division: 3
print(a % b)   # Modulus (remainder): 1
print(a ** b)  # Exponentiation: 1000
```


" %}

{% include question.html header="Comparison Operators" text="

```python
x = 5
y = 10

print(x == y)   # Equal: False
print(x != y)   # Not equal: True
print(x < y)    # Less than: True
print(x > y)    # Greater than: False
print(x <= y)   # Less than or equal: True
print(x >= y)   # Greater than or equal: False
```
" %}

{% include question.html header="Logical Operators" text="

```python
is_sunny = True
is_warm = False

print(is_sunny and is_warm)  # False
print(is_sunny or is_warm)   # True
print(not is_sunny)          # False
```
" %}

{% include question.html header="Assignment Operators" text="

```python
counter = 0
counter += 5    # Same as: counter = counter + 5
counter -= 2    # Same as: counter = counter - 2
counter *= 3    # Same as: counter = counter * 3
counter /= 2    # Same as: counter = counter / 2

print(counter)  # Output: 4.5
```
" %}
