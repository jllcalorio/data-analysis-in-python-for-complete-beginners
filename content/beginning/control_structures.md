---
section: Beginning Python
nav_order: 9
title: Control structures
topics: loop, if, for, while, functions
---

Control structures determine the order in which your code executes.

{% include question.html header="The If Statements" text="

The ```if``` statements are used for conditional execution, allowing a block of code to run only if a specified condition is true (e.g., if ```temperature > 30: print "It's hot!"```). This is done to create decision-making logic in your programs.

```python
age = 18

if age >= 18:
    print(\"You are an adult\")
elif age >= 13:
    print(\"You are a teenager\")
else:
    print(\"You are a child\")

# Multiple conditions
weather = \"sunny\"
temperature = 75

if weather == \"sunny\" and temperature > 70:
    print("Perfect day for a picnic!")
elif weather == \"rainy\" or temperature < 60:
    print(\"Stay inside today\")
else:
    print(\"Decent weather\")
```
" %}

{% include question.html header="For Loops" text="

```for``` loops are employed for iteration, repeating a block of code a fixed number of times or for each item in a collection (e.g., ```for item in list_of_items: process item```). They are crucial for automating repetitive tasks.

```python
# Loop through a list
fruits = [\"apple\", \"banana\", \"orange\"]
for fruit in fruits:
    print(f\"I like {fruit}\")

# Loop through a range of numbers
for i in range(5):  # 0 to 4
    print(f\"Count: {i}\")

# Loop through a dictionary
student = {\"name\": \"Alice\", \"age\": 20, \"major\": \"CS\"}
for key, value in student.items():
    print(f\"{key}: {value}\")
```
" %}

{% include question.html header="While Loops" text="

```when``` (often found in languages like ```Kotlin``` or as ```switch``` in others) is a construct for multi-way branching, providing a cleaner alternative to nested ```if-else if``` statements when you have multiple possible conditions to check against a single value (e.g., ```when day_of_week: \"Monday\" -> print \"Start of the week\"```). This improves code readability and maintainability.

```python
# Basic while loop
count = 0
while count < 5:
    print(f\"Count is {count}\")
    count += 1

# While loop with user input
user_input = \"\"
while user_input != \"quit\":
    user_input = input(\"Enter a command (or 'quit' to exit): \")
    if user_input != \"quit\":
        print(f\"You entered: {user_input}\")
```
" %}

{% include question.html header="Functions" text="

**Functions** are *reusable blocks of code* designed to perform a specific task (e.g., ```def calculate_area(length, width): return length * width```). They are used to break down complex problems into smaller, manageable pieces, promote code reusability, and improve the organization and readability of your programs.

```python
# Basic function
def greet(name):
    return f\"Hello, {name}!\"

# Function with default parameters
def introduce(name, age=25):
    return f\"Hi, I'm {name} and I'm {age} years old.\"

# Function with multiple parameters
def calculate_area(length, width):
    area = length * width
    return area

# Using functions
message = greet(\"Alice\")
print(message)  # Hello, Alice!

intro = introduce(\"Bob\")  # Uses default age
print(intro)              # Hi, I'm Bob and I'm 25 years old.

room_area = calculate_area(10, 12)
print(f\"Room area: {room_area} square feet\")
```
" %}

{% capture text %}Note:
Remember the **indents** in your if, for, while statements and in your functions. They act as indicators for Python to recognize that the next line of code is part of the if statement or function.
{% endcapture %}
{% include card.html text=text header=\"Setup Overview\" %}
