---
section: Beginning Python
nav_order: 7
title: Dictionaries
topics: dictionary, store values, key-value pairs
---

**Dictionaries** store data in *key-value pairs*. They're perfect for organizing related information!

{% include question.html header="Creating Dictionaries" text="

**Dictionaries** are great for storing structured data — like a patient’s ```demographic information```, ```diagnosis```, and ```vital signs``` — **all in one variable**.

```python
# Empty dictionary
empty_dict = {}

# Dictionary with data
patient_record = {
    \"name\": \"John Doe\",
    \"age\": 45,
    \"sex\": \"Male\",
    \"diagnosis\": \"Hypertension\",
    \"bp\": \"140/90\",
    \"is_admitted\": True
}

print(patient_record)
# {'name': 'John Doe', 'age': 45, 'sex': 'Male', 'diagnosis': 'Hypertension', 'bp': '140/90', 'is_admitted': True}
```
" %}

{% include question.html header="Accessing Dictionary Values" text="
```python
print(patient_record[\"diagnosis\"])              # Hypertension
print(patient_record.get(\"bp\"))                 # 140/90
print(patient_record.get(\"heart_rate\", \"N/A\"))  # N/A (Default if key doesn't exist)
```

This is like checking a patient’s chart — if a piece of information doesn’t exist, Python can return a default value (e.g., “N/A”).
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
