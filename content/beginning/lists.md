---
section: Beginning Python
nav_order: 6
title: Lists
topics: list, collection, multiple data storing
---

A list is a built-in Python data structure used to store multiple items in a single variable. Lists are ordered, mutable, and can contain mixed data types.

They're one of the most useful data structures in Python!

{% include question.html header="Creating Lists" text="

Lists in Python can be of any type: integers, strings, floats, Booleans, even other lists.

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

Items in lists can be accessed using their ```index```. The index (or position) of the item in a list start at 0.

Thus, in ```pythonfruits = [\"apple\", \"banana\", \"orange\", \"grape\"]```, the index of apple is 0, and the index of banana is 1.

Weirdly, the index of the last item in the list is -1, while the 2nd to the last index is -2. Try it out in your PC!

**Tip:** In R, the index starts at 1.

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

These list methods are used when you want to:

- add item/s in the list (whether at the end or at a specific index)
- remove item/s in the list
- inspect/count items in a list
- reordering or copying items in a list

```python
fruits = [\"apple\", \"banana\"]
```
Adding items.

```python
fruits.append(\"orange\")           # Add to end
fruits.insert(1, \"grape\")         # Insert at position 1
print(fruits)                     # ['apple', 'grape', 'banana', 'orange']
```
Removing items

```python
fruits.remove(\"grape\")          # Remove specific item
last_item = fruits.pop()          # Remove and return last item
print(fruits)                     # ['apple', 'banana']
print(last_item)                  # orange
```
Other useful methods

```python
fruits.extend([\"kiwi\", \"mango\"])  # Add multiple items
print(len(fruits))                # Get length: 4
print(fruits.count(\"apple\"))      # Count occurrences: 1
```
" %}

{% include question.html header="List Slicing" text="

Slicing allows you to extract a portion of a list using a concise syntax.

It follows this syntax: ```list[start:stop:step]```

```python
numbers = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]

print(numbers[2:5])    # Items 2 to 4: [2, 3, 4]
print(numbers[:3])     # First 3 items: [0, 1, 2]
print(numbers[7:])     # From index 7 to end: [7, 8, 9]
print(numbers[::2])    # Every second item: [0, 2, 4, 6, 8]
```

You can still use indexing from the end using negative indices.

```python
numbers[-3:]    # Last 3 items: [7, 8, 9]
numbers[:-2]    # All except last 2: [0, 1, 2, 3, 4, 5, 6, 7]

numbers[::3]    # Every third item: [0, 3, 6, 9]
numbers[::-1]   # Reversed list: [9, 8, 7, ..., 0]
```

" %}
