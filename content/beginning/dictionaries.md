---
section: Beginning Python
nav_order: 7
title: Dictionaries
topics: dictionary, store values, key-value pairs
---

**Dictionaries** store data in *key-value pairs*. They're perfect for organizing related information!

# **Creating Dictionaries**
```python
# Empty dictionary
empty_dict = {}

# Dictionary with data
student = {
    "name": "Alice",
    "age": 20,
    "major": "Computer Science",
    "gpa": 3.8
}

print(student)
```

# **Accessing Dictionary Values**
```python
student = {"name": "Alice", "age": 20, "major": "Computer Science"}

# Accessing values
print(student["name"])        # Alice
print(student.get("age"))     # 20
print(student.get("grade", "Not found"))  # Default if key doesn't exist
```

# **Modifying Dictionaries**
```python
student = {"name": "Alice", "age": 20}

# Adding/updating values
student["grade"] = "A"        # Add new key-value pair
student["age"] = 21           # Update existing value

# Removing items
del student["grade"]          # Remove specific key
removed_value = student.pop("age", "Not found")  # Remove and return value

print(student)  # {"name": "Alice"}
```

# **Dictionary Methods**
```python
student = {"name": "Alice", "age": 20, "major": "CS"}

print(student.keys())      # dict_keys(['name', 'age', 'major'])
print(student.values())    # dict_values(['Alice', 20, 'CS'])
print(student.items())     # dict_items([('name', 'Alice'), ('age', 20), ('major', 'CS')])

# Check if key exists
print("name" in student)   # True
print("grade" in student)  # False
```
