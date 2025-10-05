---
section: Beginning Python
nav_order: 4
title: Basic Data Types
topics: data type, int, float, string
---

Python has several built-in data types. Understanding these is crucial for effective programming.

# **The Four Main Data Types**

{% include question.html header="Strings (str)" text="

Strings are considered as text data enclosed in single or double quotation marks.

```python
first_name = \"John\"
last_name = 'Doe'
message = \"\"\"This is a
multi-line string\"\"\"

print(type(first_name))  # Output: <class 'str'>
```
" %}

{% include question.html header="Integers (int)" text="

Integers are numbers, specifically whole numbers. These data are numbers that do not contain decimal places.

```python
age = 25
year = 2025
negative_number = -10

print(type(age))  # Output: <class 'int'>
```
" %}

{% include question.html header="Floats (float)" text="

Floats are numbers like integers. However, floats are reserved for numbers that have decimal places.

```python
price = 19.99
temperature = -5.5
pi = 3.14159

print(type(price))  # Output: <class 'float'>
```
" %}

{% include question.html header="Booleans (bool)" text="

Booleans are either 'True' or 'False' data.

```python
is_active = True
is_finished = False

print(type(is_active))  # Output: <class 'bool'>
```
" %}

{% include question.html header="On to Checking Data Types" text="

Let's check what are the data types of the given data. For example, if we have a numeric value of '42' what could be the data type?

" solution="
```python
value = 42
print(type(value))  # <class 'int'>
```
" %}

{% include question.html header="Converting Between Data Types" text="

If, for some reason, we want to convert from one data type to another, we can do that in Python as well.

In the example below, we convert the data '25' from a 'string' data type to an 'integer' data type.

```python
age_str = \"25\"
age_int = int(age_str)
print(age_int + 5)       # Output: 30
```
" %}

{% include question.html header="Integer to string" text="

We can also do vice-versa.

```python
score = 95
score_str = str(score)
print\"Your score is: \" + score_str)
```
" %}

{% include question.html header="String to float" text="
```python
price_str = \"19.99\"
price_float = float(price_str)
```
" %}

{% include question.html header="Float to integer (truncates decimal)" text="
```python
price_int = int(19.99)  # Result: 19
```
" %}

{% include question.html header="Boolean conversions" text="
```python
print(bool(1))    # True
print(bool(0))    # False
print(bool(\"\"))   # False (empty string)
print(bool(\"Hi\")) # True (non-empty string)
```
" %}
