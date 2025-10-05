---
section: Beginning Python
nav_order: 6
title: Lists
topics: list, collection, multiple data storing
---

A list is a built-in Python data structure used to store multiple items in a single variable. Lists are ordered, mutable, and can contain mixed data types.

They're one of the most useful data structures in Python!

{% include question.html header="Creating Lists" text="
```python
# Empty list
empty_list = [] # Can be used to initialize a list as a container of results

# List with items
fruits  = [\"apple\", \"banana\", \"orange\"]
numbers = [1, 2, 3, 4, 5]
mixed   = [\"hello\", 42, 3.14, True]

print(fruits)  # Output: ['apple', 'banana', 'orange']
```
" %}

{% include question.html header="Accessing List Items" text="
```python
fruits = [\"apple\", \"banana\", \"orange\", \"grape\"]

# Accessing by index (starts at 0)
print(fruits[0])   # First item:     apple
print(fruits[1])   # Second item:    banana
print(fruits[-1])  # Last item:      grape
print(fruits[-2])  # Second to last: orange
```
" %}

{% include question.html header="List Methods" text="
```python
fruits = [\"apple\", \"banana\"]

# Adding items
fruits.append(\"orange\")        # Add to end
fruits.insert(1, \"grape\")      # Insert at position 1
print(fruits)                  # ['apple', 'grape', 'banana', 'orange']

# Removing items
fruits.remove(\"grape\")         # Remove specific item
last_item = fruits.pop()       # Remove and return last item
print(fruits)                  # ['apple', 'banana']
print(last_item)               # orange

# Other useful methods
fruits.extend([\"kiwi\", \"mango\"])  # Add multiple items
print(len(fruits))                # Get length: 4
print(fruits.count(\"apple\"))      # Count occurrences: 1
```
" %}

# **List Slicing**
```python
numbers = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]

print(numbers[2:5])    # Items 2 to 4: [2, 3, 4]
print(numbers[:3])     # First 3 items: [0, 1, 2]
print(numbers[7:])     # From index 7 to end: [7, 8, 9]
print(numbers[::2])    # Every second item: [0, 2, 4, 6, 8]
```
