---
section: Intermediate Python
nav_order: 6
title: Simple Exercises with Solutions
topics: exercises
---

# Exercise 1: Advanced Calculator Module

## Create a comprehensive calculator module with error handling.

```python
# advanced_calculator.py
"""
Advanced calculator module with error handling and multiple operations.
"""

import math

def calculate(operation, *args):
    """
    Perform various mathematical operations.
    
    Args:
        operation (str): The operation to perform
        *args: Numbers to operate on
    
    Returns:
        float: Result of the operation
    """
    try:
        if operation == "add":
            return sum(args)
        elif operation == "multiply":
            result = 1
            for num in args:
                result *= num
            return result
        elif operation == "power":
            if len(args) != 2:
                raise ValueError("Power operation requires exactly 2 arguments")
            return args[0] ** args[1]
        elif operation == "sqrt":
            if len(args) != 1:
                raise ValueError("Square root requires exactly 1 argument")
            if args[0] < 0:
                raise ValueError("Cannot calculate square root of negative number")
            return math.sqrt(args[0])
        elif operation == "average":
            if not args:
                raise ValueError("Average requires at least 1 argument")
            return sum(args) / len(args)
        else:
            raise ValueError(f"Unknown operation: {operation}")
            
    except TypeError as e:
        raise TypeError(f"Invalid argument type: {e}")

def safe_calculate(operation, *args):
    """Wrapper function with error handling."""
    try:
        result = calculate(operation, *args)
        return True, result
    except Exception as e:
        return False, str(e)

# Test the module
if __name__ == "__main__":
    test_cases = [
        ("add", 1, 2, 3, 4),
        ("multiply", 2, 3, 4),
        ("power", 2, 8),
        ("sqrt", 16),
        ("average", 10, 20, 30),
        ("sqrt", -1),  # Should fail
        ("unknown", 1, 2)  # Should fail
    ]
    
    for case in test_cases:
        operation = case[0]
        numbers = case[1:]
        success, result = safe_calculate(operation, *numbers)
        
        if success:
            print(f"{operation}({', '.join(map(str, numbers))}) = {result}")
        else:
            print(f"{operation}({', '.join(map(str, numbers))}) failed: {result}")
```

# Exercise 2: Student Grade Manager

## Create a system to manage student grades with file operations and error handling.

```python
# student_manager.py
"""
Student grade management system.
"""

import json
from datetime import datetime

class GradeManager:
    def __init__(self, filename="grades.json"):
        self.filename = filename
        self.students = self.load_data()
    
    def load_data(self):
        """Load student data from file."""
        try:
            with open(self.filename, 'r') as f:
                return json.load(f)
        except FileNotFoundError:
            print(f"No existing data file found. Creating new one.")
            return {}
        except json.JSONDecodeError:
            print(f"Invalid JSON in {self.filename}. Starting fresh.")
            return {}
    
    def save_data(self):
        """Save student data to file."""
        try:
            with open(self.filename, 'w') as f:
                json.dump(self.students, f, indent=2)
            return True
        except Exception as e:
            print(f"Error saving data: {e}")
            return False
    
    def add_student(self, name, student_id):
        """Add a new student."""
        if student_id in self.students:
            raise ValueError(f"Student ID {student_id} already exists")
        
        self.students[student_id] = {
            "name": name,
            "grades": [],
            "created": datetime.now().isoformat()
        }
        self.save_data()
    
    def add_grade(self, student_id, subject, grade):
        """Add a grade for a student."""
        if student_id not in self.students:
            raise KeyError(f"Student ID {student_id} not found")
        
        if not 0 <= grade <= 100:
            raise ValueError("Grade must be between 0 and 100")
        
        self.students[student_id]["grades"].append({
            "subject": subject,
            "grade": grade,
            "date": datetime.now().isoformat()
        })
        self.save_data()
    
    def get_average(self, student_id):
        """Calculate student's average grade."""
        if student_id not in self.students:
            raise KeyError(f"Student ID {student_id} not found")
        
        grades = self.students[student_id]["grades"]
        if not grades:
            return 0
        
        total = sum(g["grade"] for g in grades)
        return total / len(grades)
    
    def get_student_report(self, student_id):
        """Generate a report for a student."""
        if student_id not in self.students:
            raise KeyError(f"Student ID {student_id} not found")
        
        student = self.students[student_id]
        average = self.get_average(student_id)
        
        report = f"Student Report for {student['name']} (ID: {student_id})\n"
        report += f"Average Grade: {average:.2f}\n"
        report += "Individual Grades:\n"
        
        for grade_info in student["grades"]:
            report += f"  {grade_info['subject']}: {grade_info['grade']}\n"
        
        return report

# Usage example
if __name__ == "__main__":
    manager = GradeManager()
    
    try:
        # Add students
        manager.add_student("Alice Johnson", "S001")
        manager.add_student("Bob Smith", "S002")
        
        # Add grades
        manager.add_grade("S001", "Math", 85)
        manager.add_grade("S001", "Science", 92)
        manager.add_grade("S001", "English", 78)
        
        manager.add_grade("S002", "Math", 90)
        manager.add_grade("S002", "Science", 87)
        
        # Generate reports
        print(manager.get_student_report("S001"))
        print(manager.get_student_report("S002"))
        
    except Exception as e:
        print(f"Error: {e}")
```

# Exercise 3: Data Processing Pipeline

## Create a data processing pipeline with functions and error handling.

```python
# data_pipeline.py
"""
Data processing pipeline with validation and transformation functions.
"""

from datetime import datetime
import re

def validate_email(email):
    """Validate email format."""
    pattern = r'^[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}$'
    return re.match(pattern, email.strip()) is not None

def validate_phone(phone):
    """Validate phone number format."""
    # Remove all non-digit characters
    cleaned = re.sub(r'\D', '', phone)
    # Check if it's 10 digits
    return len(cleaned) == 10

def clean_data(raw_data):
    """Clean and validate raw data."""
    cleaned_records = []
    errors = []
    
    for i, record in enumerate(raw_data):
        try:
            # Create cleaned record
            cleaned_record = {}
            
            # Clean name
            if "name" not in record or not record["name"].strip():
                raise ValueError("Name is required")
            cleaned_record["name"] = record["name"].strip().title()
            
            # Validate and clean email
            if "email" not in record:
                raise ValueError("Email is required")
            if not validate_email(record["email"]):
                raise ValueError("Invalid email format")
            cleaned_record["email"] = record["email"].strip().lower()
            
            # Validate and clean phone
            if "phone" in record:
                if not validate_phone(record["phone"]):
                    raise ValueError("Invalid phone number")
                # Format phone number
                digits = re.sub(r'\D', '', record["phone"])
                cleaned_record["phone"] = f"({digits[:3]}) {digits[3:6]}-{digits[6:]}"
            
            # Clean age
            if "age" in record:
                age = int(record["age"])
                if not 0 <= age <= 120:
                    raise ValueError("Age must be between 0 and 120")
                cleaned_record["age"] = age
            
            cleaned_record["processed_date"] = datetime.now().isoformat()
            cleaned_records.append(cleaned_record)
            
        except Exception as e:
            errors.append(f"Record {i+1}: {e}")
    
    return cleaned_records, errors

def generate_summary(records):
    """Generate summary statistics from cleaned records."""
    if not records:
        return {"total": 0, "message": "No records to summarize"}
    
    summary = {
        "total_records": len(records),
        "has_phone": sum(1 for r in records if "phone" in r),
        "has_age": sum(1 for r in records if "age" in r),
    }
    
    # Age statistics
    ages = [r["age"] for r in records if "age" in r]
    if ages:
        summary["age_stats"] = {
            "average": sum(ages) / len(ages),
            "min": min(ages),
            "max": max(ages)
        }
    
    # Email domain analysis
    domains = {}
    for record in records:
        domain = record["email"].split("@")[1]
        domains[domain] = domains.get(domain, 0) + 1
    
    summary["top_domains"] = sorted(domains.items(), key=lambda x: x[1], reverse=True)[:5]
    
    return summary

# Example usage and testing
if __name__ == "__main__":
    # Sample raw data with various issues
    raw_data = [
        {"name": "alice johnson", "email": "alice@example.com", "phone": "555-123-4567", "age": "25"},
        {"name": "  bob smith  ", "email": "BOB@EXAMPLE.COM", "phone": "5551234567", "age": "30"},
        {"name": "", "email": "invalid-email", "phone": "123", "age": "150"},  # Multiple errors
        {"name": "Charlie Brown", "email": "charlie@test.org", "age": "22"},  # No phone
        {"name": "Diana Prince", "email": "diana@amazon.com", "phone": "(555) 987-6543", "age": "-5"},  # Invalid age
    ]
    
    print("Processing raw data...")
    cleaned_records, errors = clean_data(raw_data)
    
    print(f"\nSuccessfully processed {len(cleaned_records)} records")
    print(f"Encountered {len(errors)} errors")
    
    if errors:
        print("\nErrors encountered:")
        for error in errors:
            print(f"  - {error}")
    
    if cleaned_records:
        print("\nCleaned records:")
        for record in cleaned_records:
            print(f"  {record}")
        
        print("\nSummary statistics:")
        summary = generate_summary(cleaned_records)
        for key, value in summary.items():
            print(f"  {key}: {value}")
```

# Exercise 4: Configuration Manager

## Create a configuration management system using modules and error handling.

```python
# config_manager.py
"""
Configuration management system with validation and defaults.
"""

import json
import os
from typing import Any, Dict, Optional

class ConfigError(Exception):
    """Custom exception for configuration errors."""
    pass

class ConfigManager:
    """Manage application configuration with validation and defaults."""
    
    def __init__(self, config_file="config.json"):
        self.config_file = config_file
        self.defaults = {
            "database": {
                "host": "localhost",
                "port": 5432,
                "name": "myapp",
                "timeout": 30
            },
            "api": {
                "base_url": "https://api.example.com",
                "timeout": 10,
                "rate_limit": 100
            },
            "logging": {
                "level": "INFO",
                "file": "app.log",
                "max_size": "10MB"
            }
        }
        self.config = self.load_config()
    
    def load_config(self) -> Dict[str, Any]:
        """Load configuration from file with fallback to defaults."""
        try:
            if os.path.exists(self.config_file):
                with open(self.config_file, 'r') as f:
                    file_config = json.load(f)
                # Merge with defaults
                return self._merge_configs(self.defaults, file_config)
            else:
                print(f"Config file {self.config_file} not found. Using defaults.")
                return self.defaults.copy()
        except json.JSONDecodeError as e:
            raise ConfigError(f"Invalid JSON in config file: {e}")
        except Exception as e:
            raise ConfigError(f"Error loading config: {e}")
    
    def _merge_configs(self, defaults: Dict, overrides: Dict) -> Dict:
        """Recursively merge configuration dictionaries."""
        result = defaults.copy()
        for key, value in overrides.items():
            if key in result and isinstance(result[key], dict) and isinstance(value, dict):
                result[key] = self._merge_configs(result[key], value)
            else:
                result[key] = value
        return result
    
    def get(self, key_path: str, default: Any = None) -> Any:
        """Get configuration value using dot notation."""
        try:
            keys = key_path.split('.')
            value = self.config
            for key in keys:
                value = value[key]
            return value
        except (KeyError, TypeError):
            if default is not None:
                return default
            raise ConfigError(f"Configuration key '{key_path}' not found")
    
    def set(self, key_path: str, value: Any) -> None:
        """Set configuration value using dot notation."""
        keys = key_path.split('.')
        config = self.config
        
        # Navigate to the parent of the target key
        for key in keys[:-1]:
            if key not in config:
                config[key] = {}
            config = config[key]
        
        # Set the final value
        config[keys[-1]] = value
    
    def validate_config(self) -> tuple[bool, list[str]]:
        """Validate current configuration."""
        errors = []
        
        try:
            # Validate database config
            db_port = self.get("database.port")
            if not isinstance(db_port, int) or not 1 <= db_port <= 65535:
                errors.append("database.port must be an integer between 1 and 65535")
            
            db_timeout = self.get("database.timeout")
            if not isinstance(db_timeout, int) or db_timeout <= 0:
                errors.append("database.timeout must be a positive integer")
            
            # Validate API config
            api_timeout = self.get("api.timeout")
            if not isinstance(api_timeout, int) or api_timeout <= 0:
                errors.append("api.timeout must be a positive integer")
            
            rate_limit = self.get("api.rate_limit")
            if not isinstance(rate_limit, int) or rate_limit <= 0:
                errors.append("api.rate_limit must be a positive integer")
            
            # Validate logging config
            log_level = self.get("logging.level")
            valid_levels = ["DEBUG", "INFO", "WARNING", "ERROR", "CRITICAL"]
            if log_level not in valid_levels:
                errors.append(f"logging.level must be one of {valid_levels}")
                
        except ConfigError as e:
            errors.append(str(e))
        
        return len(errors) == 0, errors
    
    def save_config(self) -> bool:
        """Save current configuration to file."""
        try:
            with open(self.config_file, 'w') as f:
                json.dump(self.config, f, indent=2)
            return True
        except Exception as e:
            print(f"Error saving config: {e}")
            return False
    
    def reset_to_defaults(self) -> None:
        """Reset configuration to defaults."""
        self.config = self.defaults.copy()
    
    def display_config(self) -> str:
        """Return formatted configuration for display."""
        return json.dumps(self.config, indent=2)

# Usage example
if __name__ == "__main__":
    try:
        # Create config manager
        config = ConfigManager("app_config.json")
        
        # Display current config
        print("Current configuration:")
        print(config.display_config())
        
        # Get specific values
        db_host = config.get("database.host")
        api_url = config.get("api.base_url")
        print(f"\nDatabase host: {db_host}")
        print(f"API URL: {api_url}")
        
        # Modify configuration
        config.set("database.port", 3306)
        config.set("api.timeout", 15)
        config.set("new_feature.enabled", True)
        
        # Validate configuration
        is_valid, validation_errors = config.validate_config()
        if is_valid:
            print("\nConfiguration is valid!")
        else:
            print("\nConfiguration errors:")
            for error in validation_errors:
                print(f"  - {error}")
        
        # Save configuration
        if config.save_config():
            print("\nConfiguration saved successfully!")
        else:
            print("\nFailed to save configuration!")
            
    except ConfigError as e:
        print(f"Configuration error: {e}")
    except Exception as e:
        print(f"Unexpected error: {e}")
```
