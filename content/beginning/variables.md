---
section: Beginning Python
nav_order: 3
title: Variables
topics: variable, data, values
---

*Variables* are like containers that store data values. In Python, you don't need to declare the type of variable explicitly - Python figures it out automatically!

# **Creating Variables**

```python
# Creating variables is simple
name = "Alice"
age = 25
height = 5.6
is_student = True

print(name)    # Output: Alice
print(age)     # Output: 25
```

# **Variable Naming Rules**

- Must start with a letter or underscore (_)
- Can contain letters, numbers, and underscores
- Case-sensitive (```name``` and ```Name``` are different)
- Cannot use Python keywords (like ```if```, ```for```, ```while```)

# **Good Variable Naming Practices**

```python
# Good variable names
user_name = "john_doe"
total_score = 95
is_valid = True

# Avoid these
x = "john_doe"  # Not descriptive
userName = "john_doe"  # Use snake_case in Python
2name = "invalid"  # Cannot start with number
```
