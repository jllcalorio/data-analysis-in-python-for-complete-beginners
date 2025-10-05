---
section: Intermediate Python
nav_order: 1
title: Writing Functions
topics: functions
---

**Functions** are the building blocks of well-organized code. They allow you to write code once and use it many times, making your programs more efficient and easier to maintain.

{% include question.html header="Function Basics Review" text="

Let's say we want to create a function that will take a person's name and greet them.

```python
def greet(name):
    \"\"\"A simple function that greets someone.\"\"\"
    return f\"Hello, {name}!\"
```

Call the function.

```python
message = greet(\"Alice\")
print(message)  # Output: Hello, Alice!
```
" %}

# Advanced Function Features

{% include question.html header="Default Parameters" text="

The function below creates a profile of a person. It asks for the person's ```name```, ```age```, ```city```, and ```occupation```.

```python
def create_profile(name, age, city=\"Unknown\", occupation=\"Student\"):
    \"\"\"Create a user profile with default values.\"\"\"
    profile = {
        \"name\": name,
        \"age\": age,
        \"city\": city,
        \"occupation\": occupation
    }
    return profile
```

Run the function using (1) default parameters and (2) custom characters

```python
profile1 = create_profile(\"Alice\", 22)
profile2 = create_profile(\"Bob\", 25, \"New York\", \"Developer\")

print(profile1)  # city and occupation use defaults
print(profile2)  # all parameters specified
```
" %}

{% include question.html header="Keyword Arguments" text="
```python
def order_pizza(size, *toppings, **details):
    \"\"\"Order a pizza with flexible arguments.\"\"\"
    print(f\"Pizza size: {size}\")
    print(f\"Toppings: {', '.join(toppings)}\")

    for key, value in details.items():
        print(f\"{key}: {value}\")

# Various ways to call the function
order_pizza(\"Large\", \"pepperoni\", \"mushrooms\",
            delivery=True, special_instructions=\"Extra cheese\")
```
" %}

{% include question.html header="Variable-Length Arguments" text="

This function below calculates the average.

```python
def calculate_average(*numbers):
    \"\"\"Calculate average of any number of arguments.\"\"\"
    if not numbers:
        return 0
    return sum(numbers) / len(numbers)
```

This function below creates a record of student information.

```python
def create_student_record(name, **info):
    \"\"\"Create a student record with flexible information.\"\"\"
    record = {\"name\": name}
    record.update(info)
    return record
```

Examples

```python
avg1 = calculate_average(85, 90, 78, 92)
avg2 = calculate_average(95, 87)

student = create_student_record(
    \"Alice\",
    age=20,
    major=\"Computer Science\",
    gpa=3.8,
    year=\"Junior\"
)
```

Let's view what the 'student' variable contains.

" solution="
```python
student
{'name': 'Alice',
 'age': 20,
 'major': 'Computer Science',
 'gpa': 3.8,
 'year': 'Junior'}
```
" %}

{% include question.html header="Lambda Functions (Anonymous Functions)" text="

This is what a regular function looks like. But for most times, this is already fine.

```python
def square(x):
    return x ** 2
```

Below is what is called a ```lambda``` function.

What are its advantages?

- **Inline definition:** You can define a function in a single line without naming it
- **Saves space:** Ideal for short, throwaway functions used once or in a small scope
- Great for Testing and Prototyping

What are the disadvantages?

- they can hurt readability if overused or used for complex logic
- if your function spans multiple operations or needs documentation, a named def function is usually better

```python
# Lambda equivalent
square_lambda = lambda x: x ** 2

# Common use with built-in functions
numbers = [1, 2, 3, 4, 5]
squared = list(map(lambda x: x ** 2, numbers))
print(squared)  # [1, 4, 9, 16, 25]

# Filtering with lambda
students = [
    {\"name\": \"Alice\", \"grade\": 85},
    {\"name\": \"Bob\", \"grade\": 92},
    {\"name\": \"Charlie\", \"grade\": 78}
]

high_performers = list(filter(lambda s: s[\"grade\"] >= 85, students))
print(high_performers)
```
" %}
