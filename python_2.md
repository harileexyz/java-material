

### **4. Inheritance: Structuring Classes with "Is-A" Relationships**

#### **4.1. Detailed Description**

**Inheritance** is a mechanism that allows a new class (**subclass** or **child class**) to acquire the attributes and methods of an existing class (**superclass** or **parent class**). This creates an "is-a" relationship and is the cornerstone of code reuse in OOP.

*   **Superclass (Parent):** The general class being inherited from (e.g., `Vehicle`).
*   **Subclass (Child):** The specialized class that inherits. It gets the features of the parent and can add its own unique ones (e.g., `Car`).

**Analogy to Remember: The Smartphone Family**
*   **Superclass:** A generic `Phone`. All phones have a `phone_number` and can `make_call()`.
*   **Subclass:** A `Smartphone`. It **is a** `Phone`, so it inherits the `phone_number` and the `make_call()` method. But it also adds its own unique features, like `browse_internet()` and `install_app()`.

**Key Python Concept: `super()`**
The `super()` function in Python gives you access to methods in a parent class from within a subclass. It is most commonly used in the `__init__` method of a subclass to call the parent's `__init__` method, ensuring that the parent part of the object is correctly initialized.

#### **4.2. Example: The `Employee` Hierarchy**

```python
# --- Superclass (Parent) ---
class Employee:
    def __init__(self, name, employee_id):
        self.name = name
        self.employee_id = employee_id

    def display_info(self):
        print(f"Name: {self.name}, ID: {self.employee_id}")

    def work(self):
        print(f"{self.name} is performing general employee duties.")

# --- Subclass (Child) ---
# Manager "is-an" Employee, so it inherits from it.
class Manager(Employee):
    def __init__(self, name, employee_id, department):
        # Call the parent's constructor to initialize name and employee_id
        super().__init__(name, employee_id)
        # Add a new attribute specific to Manager
        self.department = department

    # Add a new method specific to Manager
    def conduct_meeting(self):
        print(f"Manager {self.name} is conducting a meeting for the {self.department} department.")

# --- Main Code ---
print("--- Employee ---")
emp = Employee("Ravi", 101)
emp.display_info()
emp.work()

print("\n--- Manager ---")
mgr = Manager("Sunita", 201, "Engineering")
mgr.display_info()       # Calling inherited method
mgr.work()               # Calling inherited method
mgr.conduct_meeting()    # Calling its own method
```

#### **4.3. Live Practice Question: The `Animal` Hierarchy**

**Question:** Create a simple animal hierarchy.
1.  Create a base class `Animal` with a constructor that sets a `name` attribute and an `eat()` method that prints "[name] is eating."
2.  Create a subclass `Dog` that `inherits` from `Animal`.
3.  The `Dog` constructor should take a `name` and call the parent constructor using `super()`.
4.  Add a new method `bark()` to the `Dog` class that prints "Woof!".
5.  In your main code, create a `Dog` object and call both its `eat()` (inherited) and `bark()` (its own) methods.

#### **Solution**
```python
class Animal:
    def __init__(self, name):
        self.name = name

    def eat(self):
        print(f"{self.name} is eating.")

class Dog(Animal):
    def __init__(self, name):
        # Initialize the parent 'Animal' part of this object
        super().__init__(name)

    def bark(self):
        print("Woof!")

# Create and test the Dog object
my_dog = Dog("Buddy")
my_dog.eat()   # This method was inherited from Animal
my_dog.bark()  # This is the Dog's own method
```
---

### **5. Polymorphism: Creating Flexible and Dynamic Behavior**

#### **5.1. Detailed Description**

**Polymorphism** (meaning "many forms") is the ability of an object or method to take on different forms or behaviors depending on the context. In Python, this is most powerfully demonstrated through **method overriding** and **duck typing**.

*   **Method Overriding:** A subclass provides its own specific implementation of a method that is already defined in its superclass. The method name and parameters must be the same. When the method is called on an object, Python executes the version belonging to the object's actual class at runtime.
*   **Duck Typing:** "If it walks like a duck and quacks like a duck, then it must be a duck." Python doesn't care about the *type* of an object, only if it has the *methods* you are trying to call. This allows for incredible flexibility.

**Analogy to Remember: The "Speak" Command**
*   Imagine you have a function `make_animal_speak(animal)`.
*   If you pass a `Dog` object to this function, its `speak()` method will print "Woof!".
*   If you pass a `Cat` object to the *exact same function*, its `speak()` method will print "Meow!".
*   The `make_animal_speak` function is **polymorphic**. Its behavior changes depending on the actual type of the `animal` object it receives.

#### **5.2. Example: The `Document` Processor**

```python
# --- Superclass ---
class Document:
    def __init__(self, content):
        self.content = content

    def display(self):
        print("--- Generic Document ---")
        print(self.content)

# --- Subclasses with Overridden Methods ---
class PdfDocument(Document):
    def display(self):
        print("--- Displaying PDF Document ---")
        print(f"[PDF Content]: {self.content}")

class WordDocument(Document):
    def display(self):
        print("--- Displaying Word Document ---")
        print(f"[Word Content]: {self.content}")

# This function demonstrates polymorphism. It can accept ANY object
# that is a subclass of Document.
def print_document(document):
    print("\nSending document to printer...")
    # Dynamic Dispatch: Python calls the correct 'display' method
    # based on the actual object type at runtime.
    document.display()

# --- Main Code ---
doc1 = PdfDocument("This is my annual report.")
doc2 = WordDocument("This is a meeting agenda.")
doc3 = Document("This is a plain text file.") # An object of the parent class

print_document(doc1) # Will call PdfDocument's display()
print_document(doc2) # Will call WordDocument's display()
print_document(doc3) # Will call the original Document's display()
```

#### **5.3. Live Practice Question: The `Shape` Drawer**

**Question:** Demonstrate polymorphism with shapes.
1.  Create a base class `Shape` with a `draw()` method that prints "Drawing a generic shape."
2.  Create two subclasses, `Circle` and `Square`, that inherit from `Shape`.
3.  **Override** the `draw()` method in both subclasses to print "Drawing a circle: O" and "Drawing a square: []", respectively.
4.  In your main code, create a list containing one `Circle` object and one `Square` object. Loop through the list and call the `draw()` method on each shape.

#### **Solution**
```python
class Shape:
    def draw(self):
        print("Drawing a generic shape.")

class Circle(Shape):
    def draw(self):
        print("Drawing a circle: O")

class Square(Shape):
    def draw(self):
        print("Drawing a square: []")

# --- Main Code ---
# Create a list of different Shape objects
shapes = [Circle(), Square()]

# Loop through the list and call the same method on each object
for shape in shapes:
    # Python automatically calls the correct overridden method
    shape.draw()
```

---

### **6. Abstract Classes: Defining Incomplete Blueprints**

#### **6.1. Detailed Description**

An **abstract class** is a blueprint that is **intentionally left incomplete**. You cannot create objects from it directly. Its purpose is to serve as a common **base template** for a family of related subclasses. It can provide some implemented methods while **forcing** its children to implement others.

Python doesn't have a built-in `abstract` keyword like Java. Instead, we use the `abc` (Abstract Base Classes) module.

*   **`ABC`:** A helper class that makes a class abstract.
*   **`@abstractmethod`:** A decorator used to declare a method as abstract.

**Analogy to Remember: A "Vehicle" Blueprint**
*   You can't build "a vehicle." It's an abstract concept. You build a `Car` or a `Motorcycle`.
*   The `Vehicle` blueprint (abstract class) can define a concrete behavior like `honk_horn()` and an abstract behavior like `start_engine()`, forcing each specific vehicle to define how its engine starts.

#### **6.2. Example: The `PaymentMethod` Abstract Class**

```python
# We need to import from the 'abc' module
from abc import ABC, abstractmethod

# The abstract class inherits from ABC
class PaymentMethod(ABC):
    def __init__(self, amount):
        self.amount = amount

    # A concrete method - shared by all children
    def validate(self):
        print(f"Validating payment of Rs. {self.amount}")

    # An abstract method - children MUST implement this
    @abstractmethod
    def process_payment(self):
        pass # Abstract methods have no implementation

# --- Concrete Subclasses ---
class CreditCardPayment(PaymentMethod):
    def process_payment(self):
        print(f"Processing credit card payment for Rs. {self.amount}...")
        print("Payment Successful.")

class UpiPayment(PaymentMethod):
    def process_payment(self):
        print(f"Processing UPI payment for Rs. {self.amount}...")
        print("Payment Successful.")

# --- Main Code ---
# payment = PaymentMethod(100) # This would cause a TypeError!

cc_payment = CreditCardPayment(1500)
cc_payment.validate()      # Calling inherited concrete method
cc_payment.process_payment() # Calling child's implemented method

print()

upi_payment = UpiPayment(500)
upi_payment.validate()
upi_payment.process_payment()
```

#### **6.3. Live Practice Question: The `Employee` Abstract Class**

**Question:** Create an abstract class `Employee`.
1.  It should have a concrete method `go_to_work()` that prints "Going to the office."
2.  It should have an **abstract method** `calculate_pay()`.
3.  Create two concrete subclasses, `SalariedEmployee` and `HourlyEmployee`.
4.  Implement `calculate_pay()` in each. For `SalariedEmployee`, just return a fixed salary. For `HourlyEmployee`, calculate `hours * rate`.
5.  Test by creating objects of both concrete classes and calling both methods.

#### **Solution**
```python
from abc import ABC, abstractmethod

class Employee(ABC):
    def __init__(self, name):
        self.name = name
    
    def go_to_work(self):
        print(f"{self.name} is going to the office.")
        
    @abstractmethod
    def calculate_pay(self):
        pass

class SalariedEmployee(Employee):
    def calculate_pay(self):
        return 50000.00

class HourlyEmployee(Employee):
    def calculate_pay(self):
        hours_worked = 40
        rate = 1500
        return hours_worked * rate

# --- Main Code ---
salaried_emp = SalariedEmployee("Ravi")
salaried_emp.go_to_work()
print(f"Salary for {salaried_emp.name}: Rs. {salaried_emp.calculate_pay()}")

print()

hourly_emp = HourlyEmployee("Sunita")
hourly_emp.go_to_work()
print(f"Pay for {hourly_emp.name}: Rs. {hourly_emp.calculate_pay()}")
```

---

### **7. Exception Handling**

#### **7.1. Detailed Description**

An **exception** is an error that occurs during program execution. Python's exception handling mechanism allows you to manage these errors gracefully instead of crashing.

*   **`try` block:** You place the "risky" code here.
*   **`except` block:** This block is the "handler." It executes only if an exception of the specified type occurs in the `try` block. You can have **multiple `except` blocks** to handle different types of exceptions.
*   **`else` block (optional):** This block executes only if **no exceptions** were raised in the `try` block.
*   **`finally` block (optional):** This block is **guaranteed to execute** regardless of whether an exception occurred or not. It's used for cleanup code.

#### **7.2. Example: Handling Single and Multiple Exceptions**
```python
def process_data(data, index, divisor):
    try:
        # Risky operations
        value = data[index]
        result = value / divisor
    except IndexError:
        # Handle a single, specific exception
        print("Error: Invalid index provided.")
    except ZeroDivisionError:
        # Handle another single, specific exception
        print("Error: Cannot divide by zero.")
    except Exception as e:
        # A general catch-all for any other exceptions
        print(f"An unexpected error occurred: {e}")
    else:
        # This runs only if the 'try' block was successful
        print(f"Processing successful! Result is {result}")
    finally:
        # This ALWAYS runs
        print("--- Processing attempt finished ---")

# --- Main Code ---
my_list = [10, 20, 30]

print("Scenario 1: Success")
process_data(my_list, 1, 2)

print("\nScenario 2: Handle a single exception (IndexError)")
process_data(my_list, 5, 2)

print("\nScenario 3: Handle multiple exceptions (ZeroDivisionError)")
process_data(my_list, 1, 0)
```

#### **7.3. Live Practice Question: User Input Validator**

**Question:** Write a small program that asks the user to enter their age.
1.  Use a `try-except` block to handle the `ValueError` that occurs if the user enters text instead of a number.
2.  If the input is valid, print their age. If it's invalid, print a friendly error message.
3.  Use a `finally` block to print "Age verification complete."

#### **Solution**
```python
try:
    age_input = input("Please enter your age: ")
    age = int(age_input)
except ValueError:
    print("Error: That is not a valid number. Please enter digits only.")
else:
    print(f"Thank you. Your age is {age}.")
finally:
    print("Age verification complete.")
```
