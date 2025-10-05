---
section: Beginning Python
nav_order: 7
title: Dictionaries
topics: dictionary, store values, key-value pairs
---

**Dictionaries** store data in *key-value pairs*. They're perfect for organizing related information!

{% include question.html header="Creating Dictionaries" text="
```python
# Empty dictionary
empty_dict = {}

# Dictionary with data
student = {
    \"name\": \"Alice\",
    \"age\": 20,
    \"major\": \"Computer Science\",
    \"gpa\": 3.8
}

print(student)
```
" %}

{% include question.html header="Accessing Dictionary Values" text="
```python
print(student[\"name\"])                    # Alice
print(student.get(\"age\"))                 # 20
print(student.get(\"grade\", \"Not found\"))  # Not found (Default if key doesn't exist)
```
" %}

{% include question.html header="Modifying Dictionaries" text="

Adding/updating values

```python
student[\"grade\"] = \"A\"        # Add new key-value pair
student[\"age\"] = 21           # Update existing value

print(student)  # {'name': 'Alice', 'major': 'Computer Science', 'grade': 'A', 'age': 21}
```python

Removing items

```
del student[\"grade\"]                             # Remove specific key
removed_value = student.pop(\"age\", \"Not found\")  # Remove and return value

print(student)  # {'name': 'Alice', 'major': 'Computer Science'}
```
" %}

{% include question.html header="Dictionary Methods" text="
```python
print(student.keys())      # dict_keys(['name', 'major'])
print(student.values())    # dict_values(['Alice', 'Computer Science'])
print(student.items())     # dict_items([('name', 'Alice'), ('major', 'Computer Science')])

# Check if key exists
print(\"name\" in student)   # True
print(\"grade\" in student)  # False
```
" %}
