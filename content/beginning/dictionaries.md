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
patient_record = {
    \"name": \"John Doe\",
    \"age": 45,
    \"sex": \"Male\",
    \"diagnosis\": \"Hypertension\",
    \"bp\": \"140/90\",
    \"is_admitted\": True
}

print(patient_record)
# {'name': 'John Doe', 'age': 45, 'sex': 'Male', 'diagnosis': 'Hypertension', 'bp': '140/90', 'is_admitted': True}
```

**Dictionaries** are great for storing structured data — like a patient’s ```demographic information```, ```diagnosis```, and ```vital signs``` — **all in one variable**.
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

print(student)  # {'name': 'Alice', 'age': 21, 'major': 'Computer Science', 'gpa': 3.8, 'grade': 'A'}
```

Removing items

```python
del student[\"grade\"]                             # Remove specific key
removed_value = student.pop(\"age\", \"Not found\")  # Remove and return value

print(student)  # {'name': 'Alice', 'major': 'Computer Science', 'gpa': 3.8}
```
" %}

{% include question.html header="Dictionary Methods" text="

Get the keys

```python
print(student.keys())      # dict_keys(['name', 'major', 'gpa'])
```

Get the values

```python
print(student.values())    # dict_values(['Alice', 'Computer Science', 3.8])
```

Get the item pairs

```python
print(student.items())     # dict_items([('name', 'Alice'), ('major', 'Computer Science'), ('gpa', 3.8)])
```

Check if key exists

```python
print(\"name\" in student)   # True
print(\"grade\" in student)  # False
```
" %}
