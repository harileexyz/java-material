

## **End-to-End Study Guide: Core Object-Oriented Programming (OOP)**

This module explains the fundamental principles that define Object-Oriented Programming and how they are implemented in Java.

### **Table of Contents**
1.  Procedural vs. Object-Oriented Programming Paradigm
2.  The Four Pillars of OOP
    *   Encapsulation (The Locker)
    *   Abstraction (The TV Remote)
    *   Inheritance (The Family Trait)
    *   Polymorphism (The Shape-shifter)
3.  Object-Oriented Programming in Java
    *   Declaring Objects & Object References
    *   Introduction to Methods (Revisited)
    *   Constructors (The Object Factory)
    *   Access Modifiers (The Security Guards)
    *   The `this` Keyword (The Self-Reference)
4.  Introduction to Microservices

---

### **1. Procedural vs. Object-Oriented Programming Paradigm**

Before diving into OOP, it's essential to understand what it replaced.

#### **Procedural Programming (like C, Pascal)**
*   **Focus:** On **procedures** or **functions** (a series of steps to perform a task).
*   **Structure:** The program is divided into a set of functions. Data is often stored in separate variables and structures, which are passed to functions for processing.
*   **Data Security:** Data is typically exposed and can be modified by any function, making it less secure and harder to manage in large applications. This is often called having "active functions" and "passive data."
*   **Analogy:** Following a **recipe book**. Each recipe (function) is a set of instructions. The ingredients (data) are listed separately. You take the ingredients and apply the recipe steps to them. The ingredients themselves have no inherent behavior.

#### **Object-Oriented Programming (like Java, C++, Python)**
*   **Focus:** On **objects**, which are self-contained entities that bundle both **data (attributes)** and the **functions (methods)** that operate on that data.
*   **Structure:** The program is a collection of interacting objects. Instead of passing data to functions, you call methods *on* objects.
*   **Data Security:** Data is typically hidden or "encapsulated" within an object, protected from outside interference. This is called having "active objects."
*   **Analogy:** Building with **LEGO blocks**. Each block (object) has its own properties (color, shape) and built-in ways to connect (methods). You build a complex structure by making these blocks interact with each other, rather than following a single, long set of instructions.

| Feature            | Procedural Programming                               | Object-Oriented Programming                          |
| :----------------- | :--------------------------------------------------- | :--------------------------------------------------- |
| **Primary Unit**   | Functions                                            | Objects                                              |
| **Approach**       | Top-down (break down a task into functions)          | Bottom-up (design objects and then assemble them)    |
| **Data Handling**  | Data and functions are separate. Data is often global and exposed. | Data and functions are bundled together (Encapsulation). Data is hidden. |
| **Real-World Focus** | Less closely models the real world.                  | More closely models real-world entities and their interactions. |
| **Examples**       | C, Fortran, Pascal                                   | Java, C#, Python, C++                                |

---

### **2. The Four Pillars of OOP**

These are the four core concepts that define a language as Object-Oriented.

#### **2.1. Encapsulation (The Locker)**
**Definition:** Encapsulation is the bundling of data (attributes) and the methods that operate on that data into a single unit, known as a **class**. It also involves restricting direct access to an object's data, a concept called **data hiding**.

*   **How it's done in Java:**
    1.  Declare the class's instance variables as **`private`**. This makes them inaccessible from outside the class.
    2.  Provide **`public`** methods, known as **getters** (to read data) and **setters** (to write data).
*   **Why it's important:**
    *   **Control:** You control how the data is accessed and modified. The setter method can include validation logic (e.g., "age cannot be negative").
    *   **Security:** Protects the internal state of an object from accidental or malicious corruption.
    *   **Flexibility:** You can change the internal implementation (e.g., how a value is stored) without breaking the code that uses your class, as long as the public methods remain the same.
*   **Analogy:** A **capsule pill**. The medicine (data) is safely contained within the plastic casing (class). You don't interact with the raw powder directly; you consume the whole capsule (interact via public methods).

**Program Example:**

```java
public class BankAccount {
    // 1. Data is declared private
    private String accountNumber;
    private double balance;

    public BankAccount(String accountNumber) {
        this.accountNumber = accountNumber;
        this.balance = 0.0;
    }

    // 2. Public "getter" to safely read the balance
    public double getBalance() {
        return this.balance;
    }

    // 2. Public "setter" to safely modify the balance
    public void deposit(double amount) {
        // Validation logic inside the method
        if (amount > 0) {
            this.balance += amount;
            System.out.println("Deposit successful.");
        } else {
            System.out.println("Deposit amount must be positive.");
        }
    }
}

// In another class:
public class Main {
    public static void main(String[] args) {
        BankAccount myAccount = new BankAccount("12345");
        // myAccount.balance = -5000; // ILLEGAL! Cannot access private field directly.
        myAccount.deposit(1000); // LEGAL: Using the public method.
        myAccount.deposit(-50); // Shows "Deposit amount must be positive."
        System.out.println("Current Balance: " + myAccount.getBalance());
    }
}
```

#### **2.2. Abstraction (The TV Remote)**
**Definition:** Abstraction means hiding the complex implementation details and showing only the essential features or functionalities to the user. It focuses on **what** an object does, not **how** it does it.

*   **How it's done in Java:** Using **`abstract classes`** and **`interfaces`**.
*   **Why it's important:**
    *   **Simplicity:** Reduces complexity. The user of a class doesn't need to know its internal workings.
    *   **Reduces Impact of Change:** You can change the internal implementation (the "how") without affecting the users who depend on the abstraction (the "what").
*   **Analogy:** A **TV remote control**. You see buttons like "Power", "Volume Up", and "Channel Down" (the essential features). You don't need to know the complex circuitry, infrared signals, or frequency modulation that happens inside the remote when you press a button.

**Program Example:**
The `Vehicle` abstract class is a perfect example.

```java
// The Abstraction: We know a vehicle can start, but we don't know how.
abstract class Vehicle {
    public abstract void startEngine(); // Essential feature, but no implementation
}

// Concrete Implementation 1
class Car extends Vehicle {
    @Override
    public void startEngine() {
        System.out.println("Car engine started with a key turn."); // The "how"
    }
}

// Concrete Implementation 2
class ElectricScooter extends Vehicle {
    @Override
    public void startEngine() {
        System.out.println("Scooter started silently with a button press."); // A different "how"
    }
}

public class Main {
    public static void main(String[] args) {
        Vehicle myCar = new Car();
        Vehicle myScooter = new ElectricScooter();
        
        myCar.startEngine(); // We just call startEngine(), we don't care how it works.
        myScooter.startEngine();
    }
}
```

#### **2.3. Inheritance (The Family Trait)**
**Definition:** Inheritance is a mechanism where a new class (subclass or child class) acquires the properties and behaviors (fields and methods) of an existing class (superclass or parent class). It represents an **"is-a"** relationship.

*   **How it's done in Java:** Using the **`extends`** keyword.
*   **Why it's important:**
    *   **Code Reusability:** Avoids duplicating code. Write common attributes and methods in a parent class and reuse them in multiple child classes.
    *   **Method Overriding:** Allows for runtime polymorphism (see next section).
    *   **Establishes a Hierarchy:** Creates a logical structure among related classes.
*   **Analogy:** **Genetics**. A child inherits traits like eye color and height (attributes) from their parents. The child is a more specialized version of a human but is still fundamentally a human. A `Dog` *is an* `Animal`. It inherits the `eat()` and `sleep()` methods but adds its own unique `bark()` method.

**Program Example:**

```java
// Superclass (Parent)
class Animal {
    String name;
    public void eat() {
        System.out.println(name + " is eating.");
    }
}

// Subclass (Child) - inherits from Animal
class Dog extends Animal {
    // Dog gets the 'name' field and 'eat()' method for free!
    
    // It can also have its own unique method
    public void bark() {
        System.out.println("Woof! Woof!");
    }
}

public class Main {
    public static void main(String[] args) {
        Dog myDog = new Dog();
        myDog.name = "Buddy"; // Accessing inherited field
        myDog.eat();         // Calling inherited method
        myDog.bark();        // Calling its own method
    }
}
```

#### **2.4. Polymorphism (The Shape-shifter)**
**Definition:** Polymorphism (from Greek, meaning "many forms") is the ability of an object to take on many forms. In programming, it most often means that a single variable, parameter, or method can work with objects of different types. The most common use is when a parent class reference is used to refer to a child class object.

*   **How it's done in Java:**
    1.  **Method Overriding (Runtime Polymorphism):** A subclass provides a specific implementation for a method that is already defined in its parent class.
    2.  **Method Overloading (Compile-time Polymorphism):** Multiple methods in the same class have the same name but different parameters (different type, number, or order of parameters).
*   **Why it's important:**
    *   **Flexibility and Extensibility:** Allows you to write generic code that can work with any new subclasses you create in the future without modification.
*   **Analogy:** A person can have many roles. The same person can be an **employee**, a **parent**, and a **friend**. In each role (form), they might respond to the same "request" (method call) differently. A request to "get ready" means something different in the context of going to work versus going to a party.

**Program Example (Method Overriding):**

```java
class Shape {
    public void draw() {
        System.out.println("Drawing a generic shape.");
    }
}

class Circle extends Shape {
    @Override // Annotation indicates we are intentionally overriding
    public void draw() {
        System.out.println("Drawing a circle: O");
    }
}

class Square extends Shape {
    @Override
    public void draw() {
        System.out.println("Drawing a square: []");
    }
}

public class Main {
    public static void main(String[] args) {
        // Here's polymorphism in action!
        // A single type of variable 'Shape' can hold different types of objects.
        Shape myShape;

        myShape = new Circle();
        myShape.draw(); // At runtime, Java knows this is a Circle and calls its draw() method.

        myShape = new Square();
        myShape.draw(); // Now, Java knows this is a Square and calls its draw() method.
    }
}
```
---

### **3. Object-Oriented Programming in Java**

This section covers the specific syntax and keywords Java uses to implement OOP concepts.

#### **3.1. Declaring Objects & Object Reference**

*   **Declaring a Reference Variable:** `ClassName variableName;`
    *   This only creates a "label" or a "pointer" that can hold the memory address of an object. At this point, it holds `null`.
    *   `BankAccount myAccount;` // `myAccount` is currently `null`.
*   **Instantiating an Object:** `new ClassName();`
    *   The `new` keyword tells the JVM to allocate memory on the heap for a new object and to run its constructor.
*   **Assigning the Reference:** `variableName = new ClassName();`
    *   This makes the reference variable point to the newly created object in memory.

**Key Concept: Reference vs. Object**
The object is the actual entity living in the heap memory. The variable is just a remote control that holds the address of that object.

```java
// 1. myCar1 is a reference variable, pointing to a new Car object.
Car myCar1 = new Car("Toyota"); 

// 2. myCar2 is another reference variable.
// It is NOT a new car. It is a second remote control pointing to the *exact same* Car object.
Car myCar2 = myCar1; 

// If you change the object using myCar2...
myCar2.setModel("Honda");

// ...the change is reflected when you check using myCar1, because they point to the same object.
System.out.println(myCar1.getModel()); // Output: Honda
```

#### **3.2. Constructors (The Object Factory)**

A constructor is a special method that is automatically called when an object is created with `new`. Its main job is to initialize the object's state (its instance variables).

*   **Rules:**
    1.  A constructor's name must be **exactly the same** as the class name.
    2.  A constructor **cannot have a return type**, not even `void`.
*   **Types:**
    *   **Default Constructor:** If you don't provide any constructor, Java automatically provides a "default" one that is empty and takes no arguments.
    *   **No-Arg Constructor:** A constructor you write that takes no arguments.
    *   **Parameterized Constructor:** A constructor that takes parameters to initialize fields with specific values.

**Program Example:**

```java
public class Employee {
    String name;
    int employeeId;

    // Parameterized Constructor
    public Employee(String name, int employeeId) {
        System.out.println("Parameterized constructor called!");
        this.name = name;
        this.employeeId = employeeId;
    }

    // No-Arg Constructor
    public Employee() {
        System.out.println("No-arg constructor called!");
        this.name = "Unknown";
        this.employeeId = -1;
    }
}

public class Main {
    public static void main(String[] args) {
        // This call invokes the parameterized constructor
        Employee emp1 = new Employee("Ravi Kumar", 101);
        
        // This call invokes the no-arg constructor
        Employee emp2 = new Employee();
    }
}
```
---
---

#### **3.3. Access Modifiers (The Security Guards)**

Access modifiers in Java are keywords that determine the visibility or "scope" of a class, field (variable), or method. They are the security guards of your code, controlling which parts of your application are allowed to access other parts. Proper use of access modifiers is fundamental to achieving **encapsulation**.

Here's the breakdown, from most restrictive to least restrictive:

| Modifier    | Same Class | Same Package | Subclass (Different Package) | World (Different Package) | **Analogy** |
| :---------- | :--------: | :----------: | :--------------------------: | :-----------------------: | :--- |
| `private`   |    Yes     |      No      |              No              |            No             | Your personal diary. |
| `default`   |    Yes     |     Yes      |              No              |            No             | A note on the family fridge. |
| `protected` |    Yes     |     Yes      |             Yes              |            No             | A family heirloom passed down. |
| `public`    |    Yes     |     Yes      |             Yes              |            Yes            | A public billboard. |

*   **`default` (or package-private):** This is the access level you get if you don't write any modifier at all. It's crucial to remember that this is not the same as `public`.

---

### **A Practical Example to Demonstrate Modifiers**

To properly demonstrate the package-level restrictions, we need to imagine our code is organized into packages. Let's assume we have two packages:
1.  **`com.school.staff`**: A package for staff-related classes.
2.  **`com.school.students`**: A package for student-related classes.

#### **File 1: The `Teacher` Class (in package `com.school.staff`)**

This class will contain members with all four access modifiers.

```java
// File: com/school/staff/Teacher.java
package com.school.staff;

public class Teacher {
    // 1. PUBLIC: Accessible from anywhere.
    public String publicName = "Mr. Sharma";

    // 2. PROTECTED: Accessible within the package and by subclasses outside the package.
    protected String protectedSubject = "Mathematics";

    // 3. DEFAULT: Accessible only within the 'com.school.staff' package.
    String defaultLockerId = "Locker-123";

    // 4. PRIVATE: Accessible ONLY within this Teacher class.
    private double privateSalary = 50000.0;

    // A public method to demonstrate access within the same class.
    public void displayTeacherInfo() {
        System.out.println("--- Accessing from within the Teacher class ---");
        System.out.println("Public Name: " + this.publicName);         // Yes
        System.out.println("Protected Subject: " + this.protectedSubject); // Yes
        System.out.println("Default Locker ID: " + this.defaultLockerId);  // Yes
        System.out.println("Private Salary: " + this.privateSalary);       // Yes (This is the ONLY place this is legal)
    }
}
```

#### **File 2: The `Principal` Class (in the SAME package)**

This class is also in `com.school.staff`, so it can access `public`, `protected`, and `default` members of `Teacher`.

```java
// File: com/school/staff/Principal.java
package com.school.staff;

public class Principal {
    public void checkTeacherDetails() {
        Teacher teacher = new Teacher();
        System.out.println("\n--- Accessing from Principal class (Same Package) ---");
        
        // Accessing Teacher's members:
        System.out.println("Teacher's Public Name: " + teacher.publicName);       // Yes
        System.out.println("Teacher's Protected Subject: " + teacher.protectedSubject); // Yes
        System.out.println("Teacher's Default Locker ID: " + teacher.defaultLockerId); // Yes
        
        // System.out.println("Teacher's Private Salary: " + teacher.privateSalary); // ERROR! Cannot access private member.
    }
}
```

#### **File 3: The `HeadStudent` Class (in a DIFFERENT package, but is a subclass)**

This class is in `com.school.students` but it `extends Teacher`. This special relationship gives it access to `protected` members.

```java
// File: com/school/students/HeadStudent.java
package com.school.students;

import com.school.staff.Teacher; // Must import the Teacher class

// HeadStudent is a subclass of Teacher.
public class HeadStudent extends Teacher {
    public void checkMentorDetails() {
        System.out.println("\n--- Accessing from HeadStudent subclass (Different Package) ---");

        // Accessing inherited Teacher members:
        System.out.println("Mentor's Public Name: " + this.publicName);          // Yes
        System.out.println("Mentor's Protected Subject: " + this.protectedSubject);  // Yes (This is the key for 'protected')
        
        // System.out.println("Mentor's Default Locker ID: " + this.defaultLockerId);  // ERROR! 'default' is not accessible outside its package.
        // System.out.println("Mentor's Private Salary: " + this.privateSalary);      // ERROR! Cannot access private member.
    }
}
```

#### **File 4: The `RegularStudent` Class (in a DIFFERENT package, NOT a subclass)**

This class is completely unrelated. It's in a different package and does not extend `Teacher`. It can only see what is fully `public`.

```java
// File: com/school/students/RegularStudent.java
package com.school.students;

import com.school.staff.Teacher; // Must import the Teacher class

public class RegularStudent {
    public void seePublicInfo() {
        Teacher teacher = new Teacher();
        System.out.println("\n--- Accessing from RegularStudent class (Different Package) ---");

        // Accessing Teacher's members:
        System.out.println("Teacher's Public Name: " + teacher.publicName);         // Yes (Only public is visible)
        
        // System.out.println("Teacher's Protected Subject: " + teacher.protectedSubject); // ERROR! Not a subclass.
        // System.out.println("Teacher's Default Locker ID: " + teacher.defaultLockerId);  // ERROR! Not in the same package.
        // System.out.println("Teacher's Private Salary: " + teacher.privateSalary);      // ERROR! Cannot access private member.
    }
}
```

### **Summary of the Example**

*   **`private`** (`privateSalary`): Only the `Teacher` class itself could access this. This is perfect for sensitive data that should never be directly touched from the outside.
*   **`default`** (`defaultLockerId`): The `Principal` could see this because they are both in the `com.school.staff` package (like office colleagues). The students, being in a different package, could not.
*   **`protected`** (`protectedSubject`): The `Principal` could see it (same package). The `HeadStudent` could also see it, even from a different package, because of the `extends Teacher` relationship (the family heirloom rule). The `RegularStudent` could not.
*   **`public`** (`publicName`): Everyone, everywhere, could see the teacher's name. It's public information.

---
---

#### **3.4. The `this` Keyword (The Self-Reference)**

The `this` keyword is a reference to the **current object**—the object whose method or constructor is being called.

*   **Primary Uses:**
    1.  **To disambiguate instance variables from local variables/parameters:** When a parameter has the same name as an instance variable, `this` is used to refer to the instance variable. This is the most common use case.
    2.  **To call another constructor from a constructor (Constructor Chaining):** `this(...)` can be used to call another constructor in the same class. If used, it must be the very first statement in the constructor.

**Program Example (Illustrating both uses):**

```java
public class Student {
    private String name;
    private int age;

    // Constructor 1
    public Student(String name, int age) {
        // Use 'this' to refer to the instance variables 'name' and 'age'
        this.name = name;
        this.age = age;
    }

    // Constructor 2 (Constructor Chaining)
    public Student(String name) {
        // Calls the first constructor with a default age of 18
        this(name, 18); 
    }

    public void introduce() {
        // 'this' is implicit here: System.out.println(this.name);
        System.out.println("Hi, my name is " + name + " and I am " + age + " years old.");
    }
}
```
---

### **4. Introduction to Microservices**

While not a core OOP concept, Microservices is a modern **software architecture paradigm** that heavily relies on OOP principles.

*   **Definition:** Microservices is an architectural style that structures an application as a collection of **small, loosely coupled, independently deployable services**. Each service is self-contained and responsible for a specific business capability.
*   **Analogy:** A **large restaurant** vs. a **food court**.
    *   **Monolith (Traditional):** One large restaurant with a single giant kitchen that does everything (Italian, Mexican, Chinese). If the pizza oven breaks, the whole kitchen might slow down. It's hard to update just the Chinese menu without affecting everything else.
    *   **Microservices:** A food court with separate, independent stalls (a pizza place, a taco stand, a noodle bar). Each stall is its own small business (service) with its own kitchen and staff. The pizza place can update its menu or even shut down for repairs without affecting the taco stand. They communicate via a common system (customers placing orders).
*   **Relation to OOP:**
    *   Each microservice is like a well-defined **object** (or a set of related objects) with a clear responsibility.
    *   **Encapsulation:** Each service encapsulates its own data (database) and logic. Other services can't access its database directly; they must communicate through a well-defined public API (like an object's public methods).
    *   **Abstraction:** The user of a service only needs to know its API (the "what"), not how it's implemented internally (the "how").
