---
section: Beginning Python
nav_order: 4
title: Basic Data Types
topics: data type, int, float, string
---

# **Basic Data Types**

Python has several built-in data types. Understanding these is crucial for effective programming.

# **The Four Main Data Types**

## Strings (str)

Text data enclosed in quotes:

```python
first_name = "John"
last_name = 'Doe'
message = """This is a 
multi-line string"""

print(type(first_name))  # Output: <class 'str'>
```

## Integers (int)

Whole numbers:

```python
age = 25
year = 2025
negative_number = -10

print(type(age))  # Output: <class 'int'>
```

## Floats (float)

Decimal numbers:

```python
price = 19.99
temperature = -5.5
pi = 3.14159

print(type(price))  # Output: <class 'float'>
```

## Booleans (bool)

True or False values:

```python
is_active = True
is_finished = False

print(type(is_active))  # Output: <class 'bool'>
```

# **Checking Data Types**

```python
value = 42
print(type(value))  # <class 'int'>
print(isinstance(value, int))  # True
```

# **Converting Between Data Types**

```python
# String to integer
age_str = "25"
age_int = int(age_str)
print(age_int + 5)  # Output: 30
```

## Integer to string

```
score = 95
score_str = str(score)
print("Your score is: " + score_str)
```

## String to float
```
price_str = "19.99"
price_float = float(price_str)
```

## Float to integer (truncates decimal)
```
price_int = int(19.99)  # Result: 19
```

## Boolean conversions
```
print(bool(1))    # True
print(bool(0))    # False
print(bool(""))   # False (empty string)
print(bool("Hi")) # True (non-empty string)
```
