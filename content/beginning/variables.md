---
section: Beginning Python
nav_order: 3
title: Variables
topics: variable, data, values, comments
---

*Variables* are like containers that store data values. In Python, you don't need to declare the type of variable explicitly - Python figures it out automatically!

# **Creating Variables**

Creating variables is simple.

```python
name = "Alice"
age = 25
height = 5.6
is_student = True

print(name)    # Output: Alice
print(age)     # Output: 25
```

# **Variable Naming Rules**

- Must start with a letter or underscore (_)
- Avoid using a single underscore as a variable name
- Can contain letters, numbers, and underscores
- Case-sensitive (```name``` and ```Name``` are different)
- Cannot use Python keywords (like ```if```, ```for```, ```while```, ```class```, ```def```, ```list```, ```str```)
- Avoid names starting and ending with double underscores (```__init__```, ```__str__```). These are reserved for **special methods** in Python classes
- Use lowercase letters with underscores (snake_case) for variable names
- Make names meaningful and specific to their purpose
- Avoid abbreviations unless they're widely understood (```num``` is okay, ```nm``` is not)

# **Good Variable Naming Practices**

Good variable names

```python
user_name = "john_doe"
total_score = 95
is_valid = True
```

Avoid these

```python
x = "john_doe"         # Not descriptive
userName = "john_doe"  # Use snake_case in Python
2name = "invalid"      # Cannot start with number
```
