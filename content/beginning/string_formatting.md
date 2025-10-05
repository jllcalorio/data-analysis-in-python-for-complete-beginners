---
section: Beginning Python
nav_order: 8
title: String Formatting
topics: string, format
---

Professional string formatting makes your output **clean and readable**.

{% include question.html header="f-strings (Recommended - Python 3.6+)" text="

Set the data.

```python
name = \"Alice\"
age = 25
score = 87.5
```
Basic f-string formatting

```python
message = f\"Hello, {name}! You are {age} years old.\"
print(message)  # Hello, Alice! You are 25 years old.
```

Formatting numbers

```python
print(f\"Your score is {score:.1f}%\")  # Your score is 87.5%
print(f\"Your score is {score:.0f}%\")  # Your score is 88%
```
" %}

{% include question.html header=".format() Method" text="
```python
name = \"Bob\"
age  = 30

message = \"Hello, {}! You are {} years old.\".format(name, age)
print(message) # Hello, Bob! You are 30 years old.
```
" %}

{% include question.html header="String Methods" text="

Printing methods for strings.

```python
text = \"  Hello World  \"

print(text)                              #   Hello World  
print(text.upper())                      #   HELLO WORLD  
print(text.lower())                      #   hello world  
print(text.strip())                      # Hello World (removes whitespace)
print(text.replace(\"World\", \"Python\"))  #   Hello Python  
```

Splitting and joining

```python
sentence = \"apple,banana,orange\"
fruits   = sentence.split(\",\")   # ['apple', 'banana', 'orange']
rejoined = \" | \".join(fruits)    # apple | banana | orange

print(sentence)   # apple,banana,orange
print(fruits)     # ['apple', 'banana', 'orange']
print(rejoined)   # apple | banana | orange
```
" %}
