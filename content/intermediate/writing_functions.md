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
```python
def calculate_average(*numbers):
    \"\"\"Calculate average of any number of arguments.\"\"\"
    if not numbers:
        return 0
    return sum(numbers) / len(numbers)

def create_student_record(name, **info):
    \"\"\"Create a student record with flexible information.\"\"\"
    record = {\"name\": name}
    record.update(info)
    return record

# Examples
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
" %}

## Lambda Functions (Anonymous Functions)
```python
# Regular function
def square(x):
    return x ** 2

# Lambda equivalent
square_lambda = lambda x: x ** 2

# Common use with built-in functions
numbers = [1, 2, 3, 4, 5]
squared = list(map(lambda x: x ** 2, numbers))
print(squared)  # [1, 4, 9, 16, 25]

# Filtering with lambda
students = [
    {"name": "Alice", "grade": 85},
    {"name": "Bob", "grade": 92},
    {"name": "Charlie", "grade": 78}
]

high_performers = list(filter(lambda s: s["grade"] >= 85, students))
print(high_performers)
```

## Function Documentation and Type Hints
```python
def calculate_compound_interest(principal: float, rate: float,
                              time: int, compound_frequency: int = 1) -> float:
    """
    Calculate compound interest.

    Args:
        principal (float): Initial amount of money
        rate (float): Annual interest rate (as decimal, e.g., 0.05 for 5%)
        time (int): Time period in years
        compound_frequency (int): How many times interest compounds per year

    Returns:
        float: Final amount after compound interest

    Example:
        >>> calculate_compound_interest(1000, 0.05, 10, 4)
        1643.62
    """
    amount = principal * (1 + rate/compound_frequency) ** (compound_frequency * time)
    return round(amount, 2)

# Usage
final_amount = calculate_compound_interest(1000, 0.05, 10, 4)
print(f"Final amount: ${final_amount}")
```

## Higher-Order Functions
```python
def apply_operation(numbers, operation):
    """Apply an operation to a list of numbers."""
    return [operation(num) for num in numbers]

def create_multiplier(factor):
    """Create a function that multiplies by a specific factor."""
    def multiplier(x):
        return x * factor
    return multiplier

# Usage
numbers = [1, 2, 3, 4, 5]

# Using built-in functions
doubled = apply_operation(numbers, lambda x: x * 2)
squared = apply_operation(numbers, lambda x: x ** 2)

# Using created functions
multiply_by_3 = create_multiplier(3)
tripled = apply_operation(numbers, multiply_by_3)

print(f"Original: {numbers}")
print(f"Doubled: {doubled}")

print(f"Squared: {squared}")
print(f"Tripled: {tripled}")
```
