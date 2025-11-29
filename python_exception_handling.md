Of course. Here is a detailed set of notes specifically covering exception handling in Python, focusing on handling single vs. multiple exceptions. This guide is structured for teaching, with clear analogies, step-by-step code examples, and integrated practice questions.

---
---

## **End-to-End Study Guide: Exception Handling in Python**

**Objective:** To understand what exceptions are, why they are important, and how to use Python's `try...except` blocks to handle both single and multiple types of errors gracefully.

### **Table of Contents**

1.  **What is an Exception?** The Safety Net Analogy
2.  **Handling a Single Exception:** The `try...except` Block
3.  **Handling Multiple Exceptions:** Using Multiple `except` Blocks
4.  **The `else` and `finally` Clauses:** Completing the Picture
5.  Common Built-in Exceptions in Python
6.  Practice Questions & Solutions

---
---

### **1. What is an Exception?**

#### **1.1. Detailed Description**

An **exception** is an error that occurs during the execution of a program. When an error happens, the normal, line-by-line flow of the program is disrupted. If this error is not "handled," the Python interpreter will stop, print an error message (called a "traceback"), and the program will crash.

Exception handling is the process of responding to these errors in a controlled way, allowing your program to continue running or to terminate gracefully with a user-friendly message.

*   **Analogy to Remember: Driving with a Safety Net**
    *   **Normal Flow:** Driving your car down a perfectly smooth road.
    *   **Exception:** Your car suddenly hits a large, unexpected pothole (`ValueError`, `TypeError`, etc.).
    *   **No Exception Handling (Crashing):** The pothole breaks your car's axle. You are stuck, and your journey is over. The program crashes.
    *   **With Exception Handling (`try...except`):** You have a high-tech suspension system (the `try...except` block) designed for this. When you hit the pothole, the suspension absorbs the shock (`except` catches the error). The car's computer might display a message, "Pothole detected, drive with care!" (`print("Error...")`), but you can **continue your journey**. Your program doesn't crash.

---

### **2. Handling a Single Exception: The `try...except` Block**

The fundamental tool for exception handling in Python is the `try...except` block.

*   **`try` block:** You place the "risky" code inside this block—the code that you anticipate *might* cause an exception.
*   **`except` block:** This block contains the code that will run **only if** an exception of the specified type occurs inside the `try` block. It is the error handler or the "safety net."

**Syntax:**
```python
try:
    # Risky code goes here
    ...
except ExceptionType:
    # Code to handle the error goes here
    ...
```

#### **2.1. Example: Handling a `ValueError`**

A `ValueError` occurs when an operation receives an argument of the correct type but an inappropriate value. A very common case is trying to convert a non-numeric string to an integer.

```python
# Program to calculate a user's birth year.
print("--- Birth Year Calculator ---")

try:
    # --- TRY BLOCK: Risky operations ---
    age_input = input("Please enter your age: ")
    
    # This line might cause a ValueError if the input is not a number.
    age = int(age_input) 
    
    birth_year = 2023 - age
    print(f"You were likely born in the year {birth_year}.")
    
except ValueError:
    # --- EXCEPT BLOCK: This code runs ONLY if a ValueError occurs ---
    print("Error: Invalid input. Please enter your age using numbers only (e.g., 25).")

print("\nProgram finished.")
```

**Live Class Walkthrough:**
1.  **Run 1 (Success):** Enter `25`. The `try` block completes successfully. The `except` block is **skipped**.
    *   **Output:** `You were likely born in the year 1998.`
2.  **Run 2 (Failure):** Enter `twenty-five`.
    *   The `int(age_input)` line fails and raises a `ValueError`.
    *   Python immediately stops executing the `try` block and jumps to the matching `except ValueError:` block.
    *   **Output:** `Error: Invalid input. Please enter your age using numbers only (e.g., 25).`
    *   Crucially, the program does not crash and continues to the final "Program finished" line.

---

### **3. Handling Multiple Exceptions**

A single `try` block can have multiple potential errors. You can handle them in two main ways:

#### **3.1. Method 1: Multiple `except` Blocks (Preferred)**

This is the best approach when you want to perform **different actions for different types of errors**. You provide a separate `except` block for each specific exception you want to handle.

**Syntax:**
```python
try:
    # Risky code
    ...
except FirstExceptionType:
    # Handle the first type of error
    ...
except SecondExceptionType:
    # Handle the second type of error
    ...
```

**Example: A Simple Division Calculator**
This program can fail in two ways:
1.  `ValueError`: If the user enters text instead of a number.
2.  `ZeroDivisionError`: If the user enters `0` for the divisor.

```python
print("--- Simple Division Calculator ---")

try:
    numerator_str = input("Enter the numerator: ")
    numerator = int(numerator_str)

    divisor_str = input("Enter the divisor: ")
    divisor = int(divisor_str)

    # This line could cause a ZeroDivisionError
    result = numerator / divisor
    print(f"The result is: {result}")

except ValueError:
    # This block handles only ValueError
    print("Error: Please enter valid numbers only.")
    
except ZeroDivisionError:
    # This block handles only ZeroDivisionError
    print("Error: Cannot divide by zero. Please enter a non-zero divisor.")

print("\nProgram finished.")
```
**Live Class Walkthrough:**
*   Run with inputs `10` and `2` (Success).
*   Run with inputs `ten` and `2` (Triggers `ValueError`).
*   Run with inputs `10` and `0` (Triggers `ZeroDivisionError`).

#### **3.2. Method 2: A Single `except` Block with a Tuple of Exceptions**

This approach is useful when you want to perform the **same action for multiple types of errors**.

**Syntax:**
```python
try:
    # Risky code
    ...
except (FirstExceptionType, SecondExceptionType) as e:
    # Handle both types of errors with the same code
    ...
```

**Example:**
```python
print("--- Simple Division Calculator (Tuple Method) ---")
try:
    numerator = int(input("Enter the numerator: "))
    divisor = int(input("Enter the divisor: "))
    result = numerator / divisor
    print(f"The result is: {result}")
    
except (ValueError, ZeroDivisionError) as e:
    # Handle both errors with a generic message
    print(f"An error occurred: Please enter valid numbers and a non-zero divisor.")
    # The 'as e' part captures the exception object, which is useful for logging.
    print(f"(Error details: {e})")

print("\nProgram finished.")
```
**Teaching Point:** Explain that the first method (multiple `except` blocks) is generally better because it allows you to give more specific, helpful error messages to the user. The second method is a convenient shortcut for generic error handling.

---

### **4. The `else` and `finally` Clauses**

*   **`else` block:** An optional block that executes **only if the `try` block completes successfully** (i.e., no exceptions were raised).
*   **`finally` block:** An optional block that is **guaranteed to execute** at the end, no matter what—whether an exception occurred, was handled, or not.

**Analogy: A Risky Mission**
*   **`try`**: Perform the risky mission.
*   **`except`**: The backup plan if the mission fails.
*   **`else`**: The "mission successful" celebration party. This only happens if the backup plan wasn't needed.
*   **`finally`**: The debriefing report. This must be filed whether the mission succeeded or failed.

**Example:**
```python
try:
    num = int(input("Enter a number to divide 100 by: "))
    result = 100 / num
except ValueError:
    print("That was not a valid number.")
except ZeroDivisionError:
    print("You cannot divide by zero.")
else:
    # This only runs if the 'try' block was successful.
    print(f"Success! The result is {result}")
finally:
    # This ALWAYS runs.
    print("Calculation attempt is complete.")
```

---

### **5. Common Built-in Exceptions in Python**
*   **`ValueError`:** Inappropriate value for a type (e.g., `int("abc")`).
*   **`TypeError`:** Operation applied to an object of an inappropriate type (e.g., `"hello" + 5`).
*   **`IndexError`:** Sequence index is out of range (e.g., `my_list[10]` on a list of size 3).
*   **`KeyError`:** Dictionary key is not found (e.g., `my_dict['unknown_key']`).
*   **`ZeroDivisionError`:** Division or modulo by zero.
*   **`FileNotFoundError`:** Trying to open a file that does not exist.

---
---

### **Practice Questions & Solutions**

#### **Practice Question 1: List Element Accessor**

**Question:** Write a function `get_element(my_list, index)` that attempts to access and print an element from a list at a given index.
1.  The function should take a list and an integer index as arguments.
2.  Use a `try-except` block to handle a potential `IndexError`.
3.  If the access is successful, print the element.
4.  If an `IndexError` occurs, print a friendly error message like "Error: Index is out of bounds."
5.  Test your function with both a valid and an invalid index.

#### **Solution**
```python
def get_element(my_list, index):
    """
    Attempts to access and print an element from a list, handling IndexError.
    """
    try:
        element = my_list[index]
        print(f"Element at index {index} is: {element}")
    except IndexError:
        print(f"Error: Index {index} is out of bounds for the given list.")

# --- Testing ---
data = ["apple", "banana", "cherry"]

print("--- Test 1: Valid Index ---")
get_element(data, 1)

print("\n--- Test 2: Invalid Index ---")
get_element(data, 5)
```
**Expected Output:**
```
--- Test 1: Valid Index ---
Element at index 1 is: banana

--- Test 2: Invalid Index ---
Error: Index 5 is out of bounds for the given list.
```

---

#### **Practice Question 2: Dictionary Value Retriever**

**Question:** Write a function `get_student_score(scores_dict, student_name)` that looks up a student's score in a dictionary.
1.  The function should take a dictionary (where keys are student names and values are scores) and a student name as arguments.
2.  Use a `try-except` block to handle a potential `KeyError` if the student's name is not in the dictionary.
3.  If the student is found, print their score.
4.  If a `KeyError` occurs, print a message like "Error: Student '[name]' not found."
5.  Use a `finally` block to always print "Score lookup complete."

#### **Solution**
```python
def get_student_score(scores_dict, student_name):
    """
    Looks up a student's score in a dictionary, handling KeyError.
    """
    try:
        score = scores_dict[student_name]
        print(f"Score for {student_name}: {score}")
    except KeyError:
        print(f"Error: Student '{student_name}' not found.")
    finally:
        print("Score lookup complete.")

# --- Testing ---
student_scores = {
    "Ravi": 88,
    "Sunita": 92,
    "Amit": 75
}

print("--- Test 1: Valid Student ---")
get_student_score(student_scores, "Sunita")

print("\n--- Test 2: Invalid Student ---")
get_student_score(student_scores, "Vikram")
```
**Expected Output:**
```
--- Test 1: Valid Student ---
Score for Sunita: 92
Score lookup complete.

--- Test 2: Invalid Student ---
Error: Student 'Vikram' not found.
Score lookup complete.
```

Of course. Including a list of common built-in exceptions is crucial for students to recognize the types of errors they will encounter. Here is an expanded section that can be added to your study guide, detailing the most important Python exceptions and their uses.

---
---

### **A Guide to Common Built-in Exceptions in Python**

While Python has a large hierarchy of exceptions, you will encounter a specific set of them very frequently. Understanding what causes them is key to writing robust code and debugging effectively. All these exceptions inherit from the base `Exception` class.

Here is a list of the most common exceptions, their causes, and code examples that would trigger them.

---

#### **1. `SyntaxError`**

*   **What it is:** This is a special kind of error that occurs *before* your program even starts running. It's raised by the Python parser when it finds code that violates the language's grammar rules.
*   **Common Causes:**
    *   Missing colons (`:`) after `if`, `for`, `def`, or `class` statements.
    *   Unmatched parentheses, brackets, or braces (`(`, `[`, `{`).
    *   Incorrect indentation.
    *   Misspelled keywords.
*   **Example:**
    ```python
    # Missing colon after the if statement
    if 5 > 3
        print("Hello") 
    # Output: SyntaxError: expected ':'
    ```

---

#### **2. `IndentationError`**

*   **What it is:** A subclass of `SyntaxError`. It occurs when a block of code is not indented correctly.
*   **Common Causes:**
    *   Inconsistent use of tabs and spaces.
    *   Not indenting code that should be in a block (e.g., inside an `if` statement or a function).
*   **Example:**
    ```python
    def my_function():
    print("This line has incorrect indentation.")
    # Output: IndentationError: expected an indented block
    ```

---

#### **3. `NameError`**

*   **What it is:** Raised when you try to use a variable or function name that has not been defined yet.
*   **Common Causes:**
    *   A typo in a variable name.
    *   Forgetting to assign a value to a variable before using it.
*   **Example:**
    ```python
    print(my_variable)
    # Output: NameError: name 'my_variable' is not defined
    ```

---

#### **4. `TypeError`**

*   **What it is:** Raised when an operation or function is applied to an object of an inappropriate type.
*   **Common Causes:**
    *   Trying to add a string and a number (`"hello" + 5`).
    *   Calling `len()` on a number (`len(123)`).
    *   Passing the wrong number of arguments to a function.
*   **Example:**
    ```python
    result = "hello" + 5
    # Output: TypeError: can only concatenate str (not "int") to str
    ```

---

#### **5. `ValueError`**

*   **What it is:** Raised when an operation or function receives an argument that has the right type but an inappropriate value.
*   **Common Causes:**
    *   Trying to convert a non-numeric string to an integer (`int("abc")`).
    *   Trying to find the index of a value that is not in a list (`my_list.index("unknown_value")`).
*   **Example:**
    ```python
    age = int("twenty-five")
    # Output: ValueError: invalid literal for int() with base 10: 'twenty-five'
    ```

---

#### **6. `IndexError`**

*   **What it is:** Raised when you try to access a sequence (like a list or a string) with an index that is out of bounds.
*   **Common Causes:**
    *   Forgetting that lists are zero-indexed.
    *   Looping one element too far.
*   **Example:**
    ```python
    my_list = ["apple", "banana", "cherry"]
    print(my_list[3]) # The valid indices are 0, 1, and 2.
    # Output: IndexError: list index out of range
    ```

---

#### **7. `KeyError`**

*   **What it is:** The dictionary equivalent of `IndexError`. It is raised when you try to access a key that does not exist in a dictionary.
*   **Common Causes:**
    *   A typo in the key name.
    *   Assuming a key exists when it might not.
*   **Example:**
    ```python
    student_scores = {"Ravi": 88, "Sunita": 92}
    print(student_scores["Amit"])
    # Output: KeyError: 'Amit'
    ```
    *   **Tip:** To avoid this, you can use the `.get()` method, which returns `None` (or a default value) if the key is not found: `print(student_scores.get("Amit"))`.

---

#### **8. `AttributeError`**

*   **What it is:** Raised when you try to access or assign to an attribute or method that doesn't exist for an object.
*   **Common Causes:**
    *   A typo in a method or attribute name.
    *   Trying to use a method from one data type on another (e.g., calling a string method on an integer).
*   **Example:**
    ```python
    my_list = [1, 2, 3]
    my_list.appendd(4) # Typo: should be 'append'
    # Output: AttributeError: 'list' object has no attribute 'appendd'
    ```

---

#### **9. `ZeroDivisionError`**

*   **What it is:** Raised when the second argument of a division or modulo operation is zero.
*   **Common Causes:**
    *   Dividing a number by a variable that happens to be zero.
*   **Example:**
    ```python
    result = 10 / 0
    # Output: ZeroDivisionError: division by zero
    ```

---

#### **10. `FileNotFoundError`**

*   **What it is:** A subclass of `IOError`/`OSError`. It is raised when you try to open a file for reading that does not exist.
*   **Common Causes:**
    *   A typo in the filename or path.
    *   The file is not in the expected directory.
*   **Example:**
    ```python
    with open("non_existent_file.txt", "r") as f:
        content = f.read()
    # Output: FileNotFoundError: [Errno 2] No such file or directory: 'non_existent_file.txt'
    ```

---

#### **11. `ImportError` / `ModuleNotFoundError`**

*   **What it is:** Raised when the Python interpreter cannot find a module you are trying to import. `ModuleNotFoundError` is a more specific subclass of `ImportError`.
*   **Common Causes:**
    *   The module is not installed in your Python environment.
    *   A typo in the module name.
*   **Example:**
    ```python
    import non_existent_module
    # Output: ModuleNotFoundError: No module named 'non_existent_module'
    ```
