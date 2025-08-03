---
section: Beginning Python
nav_order: 8
title: String Formatting
topics: string, format
---

Professional string formatting makes your output **clean and readable**.

# **f-strings (Recommended - Python 3.6+)**

```python
name  = "Alice"
age   = 25
score = 87.5

# Basic f-string formatting
message = f"Hello, {name}! You are {age} years old."
print(message)  # Hello, Alice! You are 25 years old.

# Formatting numbers
print(f"Your score is {score:.1f}%")  # Your score is 87.5%
print(f"Your score is {score:.0f}%")  # Your score is 88%
```

# **.format() Method**
```python
name = "Bob"
age  = 30

message = "Hello, {}! You are {} years old.".format(name, age)
print(message)

# With named placeholders
message = "Hello, {name}! You are {age} years old.".format(name=name, age=age)
print(message)
```

# **String Methods**
```python
text = "  Hello World  "

print(text)              #   Hello World  
print(text.upper())      # HELLO WORLD
print(text.lower())      # hello world
print(text.strip())      # Hello World (removes whitespace)
print(text.replace("World", "Python"))  # Hello Python

# Splitting and joining
sentence = "apple,banana,orange"
fruits   = sentence.split(",")   # ['apple', 'banana', 'orange']
rejoined = " | ".join(fruits)    # apple | banana | orange
```
