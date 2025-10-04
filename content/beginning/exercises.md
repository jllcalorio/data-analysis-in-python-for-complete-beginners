---
section: Beginning Python
nav_order: 10
title: Practice Exercises
topics: exercises
---

{% include question.html header="Exercise 1: Personal Information" text="Create a program that:

- Stores your personal information in variables (name, age, city)
- Calculates your birth year
- Creates a formatted introduction message
" solution="
```python
name = \"Your Name\"
age = 25
city = \"Your City\"
current_year = 2025

birth_year = current_year - age
intro = f\"Hi! I\'m {name}, I\'m {age} years old, I live in {city}, and I was born in {birth_year}.\"
print(intro)
```
" %}

{% include question.html header="Exercise 2: Shopping List Manager" text="Create a program that:

- Creates a shopping list with at least 5 items
- Adds 2 more items to the list
- Removes 1 item from the list
- Prints the final list with item numbers
" solution="
```python
shopping_list = [\"milk\", \"bread\", \"eggs\", \"apples\", \"chicken\"]
shopping_list.extend([\"rice\", \"cheese\"])
shopping_list.remove(\"bread\")

print(\"Shopping List:\")
for i, item in enumerate(shopping_list, 1):
    print(f\"{i}. {item}\")
```
" %}

{% include question.html header="Exercise 3: Grade Calculator" text="Create a program that:

- Stores student information in a dictionary
- Calculates the average grade
- Determines letter grade based on average
- Prints a formatted report
" solution="
```python
student = {
    "name": \"Alice\",
    "grades": [85, 92, 78, 96, 88]
}

average = sum(student[\"grades\"]) / len(student[\"grades\"])

if average >= 90:
    letter_grade = \"A\"
elif average >= 80:
    letter_grade = \"B\"
elif average >= 70:
    letter_grade = \"C\"
elif average >= 60:
    letter_grade = \"D\"
else:
    letter_grade = \"F\"

print(f\"Student: {student[\'name\']}\")
print(f\"Grades: {student[\'grades\']}\")
print(f\"Average: {average:.1f}\")
print(f\"Letter Grade: {letter_grade}\")
```
" %}

{% include question.html header="Exercise 4: Password Validator" text="Create a function that validates a password based on these criteria:

- At least 8 characters long
- Contains at least one number
- Contains at least one uppercase letter
" solution="
```python
def validate_password(password):
    if len(password) < 8:
        return False, \"Password must be at least 8 characters long\"
    
    has_number = any(char.isdigit() for char in password)
    has_upper = any(char.isupper() for char in password)
    
    if not has_number:
        return False, \"Password must contain at least one number\"
    
    if not has_upper:
        return False, \"Password must contain at least one uppercase letter\"
    
    return True, \"Password is valid\"

# Test the function
test_passwords = [\"weak\", \"StrongPass1\", \"nodigits\", \"NONUMBERS\"]
for pwd in test_passwords:
    is_valid, message = validate_password(pwd)
    print(f\"\'{pwd}\': {message}\")
```
" %}
