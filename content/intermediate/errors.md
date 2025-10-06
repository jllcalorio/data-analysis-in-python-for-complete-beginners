---
section: Intermediate Python
nav_order: 5
title: Errors and Exception Handling
topics: errors
---

**Errors** are inevitable in programming. Learning to handle them gracefully makes your programs robust and user-friendly.

## Types of Errors

{% include question.html header="Syntax Errors" text="

These cause syntax errors (won't run)

```python
print(\"Hello World\"
if x = 5:
    print(\"error\")
```

**Pop quiz**

Where do you think is the error, and what is causing the error?

" solution="

```python
1st line: Missing closing parenthesis
2nd line: Should be == or :
3rd line: Incorrect indentation
```
" %}

{% include question.html header="Runtime Errors (Exceptions)" text="

These cause runtime errors

```python
print(10 / 0)              # ZeroDivisionError
print(numbers[10])         # IndexError (if list has < 11 items)
print(int(\"hello\"))        # ValueError
print(undefined_variable)  # NameError
```
" %}

## Basic Exception Handling

{% include question.html header="Try-Except Blocks" text="

```python
def safe_divide(a, b):
    \"\"\"Safely divide two numbers.\"\"\"
    try:
        result = a / b
        return result
    except ZeroDivisionError:
        print(\"Error: Cannot divide by zero!\")
        return None

# Usage
result1 = safe_divide(10, 2)    # Returns 5.0
result2 = safe_divide(10, 0)    # Prints error, returns None
```
" %}

{% include question.html header="Handling Multiple Exceptions" text="

```python
def process_user_input():
    \"\"\"Process user input with error handling.\"\"\"
    try:
        age = int(input(\"Enter your age: \"))
        birth_year = 2025 - age

        if age < 0:
            raise ValueError(\"Age cannot be negative\")

        return birth_year

    except ValueError as e:
        if \"invalid literal\" in str(e):
            print(\"Please enter a valid number\")
        else:
            print(f\"Error: {e}\")
        return None
    except KeyboardInterrupt:
        print(\"\nOperation cancelled by user\")
        return None

# Usage
year = process_user_input()
if year:
    print(f\"You were born in {year}\")
```
" %}

{% include question.html header="Try-Except-Else-Finally" text="

```python
def read_file_safely(filename):
    \"\"\"Read a file with comprehensive error handling.\"\"\"
    file_handle = None
    try:
        file_handle = open(filename, 'r')
        content = file_handle.read()
        print(\"File read successfully!\")

    except FileNotFoundError:
        print(f\"Error: File '{filename}' not found\")
        content = None

    except PermissionError:
        print(f\"Error: No permission to read '{filename}'\")
        content = None

    except Exception as e:
        print(f\"Unexpected error: {e}\")
        content = None

    else:
        # This runs only if no exception occurred
        print(f\"File size: {len(content)} characters\")

    finally:
        # This always runs, even if there was an exception
        if file_handle:
            file_handle.close()
            print(\"File closed\")

    return content
```
" %}

{% include question.html header="Raising Custom Exceptions" text="

```python
class InsufficientFundsError(Exception):
    \"\"\"Custom exception for banking operations.\"\"\"
    pass

class BankAccount:
    def __init__(self, balance=0):
        self.balance = balance

    def withdraw(self, amount):
        \"\"\"Withdraw money from account.\"\"\"
        if amount <= 0:
            raise ValueError(\"Withdrawal amount must be positive\")

        if amount > self.balance:
            raise InsufficientFundsError(
                f\"Cannot withdraw ${amount}. Balance is ${self.balance}\"
            )

        self.balance -= amount
        return self.balance

# Usage
account = BankAccount(100)

try:
    account.withdraw(150)
except InsufficientFundsError as e:
    print(f\"Transaction failed: {e}\")
except ValueError as e:
    print(f\"Invalid amount: {e}\")
```
" %}

# Debugging Tips

```python
def debug_function(data):
    \"\"\"Function with debugging techniques.\"\"\"
    print(f"DEBUG: Input data type: {type(data)}")
    print(f"DEBUG: Input data value: {data}")

    try:
        # Process data
        if isinstance(data, str):
            result = data.upper()
        elif isinstance(data, (int, float)):
            result = data * 2
        elif isinstance(data, list):
            result = [item * 2 for item in data]
        else:
            raise TypeError(f"Unsupported data type: {type(data)}")

        print(f"DEBUG: Result: {result}")
        return result

    except Exception as e:
        print(f"DEBUG: Exception occurred: {e}")
        print(f"DEBUG: Exception type: {type(e).__name__}")
        raise  # Re-raise the exception

# Testing
test_data = ["hello", 42, [1, 2, 3], {"key": "value"}]
for data in test_data:
    try:
        result = debug_function(data)
        print(f"Success: {result}\n")
    except Exception as e:
        print(f"Failed: {e}\n")
```
