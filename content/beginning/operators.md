---
section: Beginning Python
nav_order: 5
title: Operators
topics: arithmetic, comparison, logical, assignment, operators
---

Operators allow you to perform operations on variables and values.

This includes mathematical operators, comparative operators, etc.

{% include question.html header="Arithmetic Operators" text="

Performing mathematical operators can be done in Python. If you remember PEMDAS, yes, it can be done.

```python
a = 10
b = 3

print(a + b)   # Addition: 13
print(a - b)   # Subtraction: 7
print(a * b)   # Multiplication: 30
print(a / b)   # Division: 3.333...
print(a // b)  # Floor division: 3 [divides 'a' by 'b' and rounds down to the nearest whole number (integer)]
print(a % b)   # Modulus (remainder): 1 [an operator that returns the remainder after dividing 'a' by 'b']
print(a ** b)  # Exponentiation: 1000, in Excel, this is a^b = 10^3
```

Remember that PEMDAS stands for?

" solution="
PEMDAS is a mathematical acronym for the order of operations, namely
- Parentheses,
- Exponents,
- Multiplication,
- Division,
- Addition, and
- Subtraction.
" %}

{% include question.html header="Comparison Operators" text="

In Python, you can compare values if they are the same or different, or if a value is larger/smaller than the other value.

If you want to check if two (2) values are the same, you should use double equal sign (==), not just one. Why? Because using one equal sign (=) corresponds to setting the left side of the equal sign to be the 'variable' name.

```python
x = 5
y = 10

print(x == y)   # Equal: False, checks if 2 values ARE EQUAL
print(x != y)   # Not equal: True, checks if 2 values ARE NOT EQUAL
print(x < y)    # Less than: True, checks if x is less than y
print(x > y)    # Greater than: False, checks if x is greater than y
print(x <= y)   # Less than or equal: True, checks if x is less than or equal to y
print(x >= y)   # Greater than or equal: False, checks if y is greater than or equal to y
```
" %}

{% include question.html header="Logical Operators" text="

Logical operators are Boolean operators used to combine or invert truth values.

```python
is_sunny = True
is_warm = False

print(is_sunny and is_warm)  # False, this checks if both values are True
print(is_sunny or is_warm)   # True, this checks if either value is True
print(not is_sunny)          # False, this inverts the Boolean value, i.e., from True to False, and False to True
```
" %}

{% include question.html header="Assignment Operators" text="

Assignment operators are used to assign values to variables and, in many cases, to update existing values using shorthand notation.

They combine a basic operation (like addition or multiplication) with assignment, making code more concise and readable.

```python
counter = 0     # Normal variable assignment, we assign the value 10 to the variable 'counter'
counter += 5    # Same as: counter = counter + 5, adds 5 to 'counter' and assigns back to 'counter'
counter -= 2    # Same as: counter = counter - 2, subtracts 2 to 'counter' and assigns back to 'counter'
counter *= 3    # Same as: counter = counter * 3, multiples 3 to 'counter' and assigns back to 'counter'
counter /= 2    # Same as: counter = counter / 2, divides 2 to 'counter' and assigns back to 'counter'

print(counter)  # Output: 4.5
```
" %}
