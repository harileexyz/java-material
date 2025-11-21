

---
---

## **End-to-End Study Guide: Introduction to the Java World**

### **Table of Contents**
1.  The Java Ecosystem: The Tools of the Trade
    *   Java Programming Environment vs. Runtime Environment
    *   The Java Compiler (`javac`)
    *   The Java Virtual Machine (JVM): The Heart of Java
2.  Structure of a Simple Java Program
3.  Primitive Data Types: The Basic Building Blocks
4.  Wrapper Types, Casting, and Autoboxing
5.  Essential Data Structures: Arrays, Strings, and Vectors

---

### **1. The Java Ecosystem: The Tools of the Trade**

Before writing code, it's essential to understand the environment where Java programs are created and executed. This ecosystem is what gives Java its famous "Write Once, Run Anywhere" capability.

#### **1.1. Java Programming Environment vs. Runtime Environment**

*   **Java Development Kit (JDK):** This is the **Programming Environment**. It's the complete toolkit for **developers**. If you want to *write* Java code, you need the JDK.
    *   **Analogy:** A full-fledged car manufacturing factory. It has all the tools, machinery, and raw materials needed to build a car from scratch.
    *   **Includes:** The JRE, the compiler (`javac`), a debugger (`jdb`), and other development tools.

*   **Java Runtime Environment (JRE):** This is the **Runtime Environment**. It provides the minimum requirements to **run** a pre-compiled Java application. If you only want to *use* a Java program, you only need the JRE.
    *   **Analogy:** The car itself, along with its engine and fuel. It has everything needed to *run*, but you can't use it to build another car.
    *   **Includes:** The JVM and the core Java libraries (the "Java API").

**The Relationship:** `JDK contains JRE, which in turn contains JVM.`
`Developer needs JDK` → `User needs JRE`

#### **1.2. The Java Compiler (`javac`)**

The Java Compiler is a program (found in the JDK) that takes your human-readable source code (a `.java` file) and translates it into a highly optimized, intermediate language called **Java Bytecode**.

*   **Input:** `MyProgram.java` (Source Code)
*   **Tool:** `javac`
*   **Output:** `MyProgram.class` (Bytecode)

This bytecode is not machine code for Windows or macOS. It's a universal language designed to be understood by only one thing: the Java Virtual Machine.

#### **1.3. The Java Virtual Machine (JVM): The Heart of Java**

The JVM is the magic component that makes Java platform-independent. It is a "virtual" computer that runs inside your actual operating system.

*   **Its Job:** To take the platform-neutral bytecode (`.class` file) and translate it into native machine code that your specific computer's processor can understand and execute.
*   **How it achieves "Write Once, Run Anywhere":** You can take the same `.class` file and run it on any device that has a JVM installed. The Windows JVM translates the bytecode to Windows machine code. The macOS JVM translates the *same* bytecode to macOS machine code. You write the code once, and the JVM handles the platform-specific translation.

**The Full Process:**
`Code (.java)` → `[javac Compiler]` → `Bytecode (.class)` → `[JVM]` → `Native Machine Code` → `Execution`

---

### **2. Structure of a Simple Java Program**

Every standalone Java application must have a specific structure to be executable.

```java
// This is a single-line comment.

/*
 * This is a multi-line comment. It's good practice to add these
 * to explain what the class does.
 */

// Every executable Java program must have at least one public class.
// The public class name MUST match the file name (e.g., HelloWorld.java).
public class HelloWorld {

    // This is the main method. It is the entry point of the program.
    // The JVM looks for this exact signature to start execution.
    // - public: So it can be called from outside the class by the JVM.
    // - static: So it can be run without creating an object of the HelloWorld class.
    // - void: The method doesn't return any value.
    // - main: The name of the method.
    // - String[] args: A parameter to receive command-line arguments.
    public static void main(String[] args) {
        
        // System.out.println() is a command to print a line of text to the console.
        System.out.println("Hello, B.Tech Students! Welcome to Java.");
        
    } // End of the main method
    
} // End of the HelloWorld class
```

**How to Run from the Command Line:**
1.  Save the code as `HelloWorld.java`.
2.  Open a terminal/command prompt.
3.  Compile the code: `javac HelloWorld.java`
4.  Run the program: `java HelloWorld`

---

### **3. Primitive Data Types: The Basic Building Blocks**

Primitive types are the most fundamental data types in Java. They are not objects and store simple values directly in memory. Java has 8 primitive types.

| Category  | Data Type | Size      | Description                               | Example Declaration               |
| :-------- | :-------- | :-------- | :---------------------------------------- | :-------------------------------- |
| **Integer** | `byte`    | 1 byte    | Stores small whole numbers (-128 to 127)  | `byte age = 25;`                  |
|           | `short`   | 2 bytes   | Stores whole numbers (-32,768 to 32,767) | `short year = 2023;`              |
|           | `int`     | 4 bytes   | The most common type for whole numbers. | `int salary = 90000;`             |
|           | `long`    | 8 bytes   | For very large whole numbers.             | `long population = 8000000000L;`  |
| **Floating-Point** | `float`   | 4 bytes   | For fractional numbers (single-precision). | `float price = 199.99f;`            |
|           | `double`  | 8 bytes   | For more precise fractional numbers (double-precision). | `double pi = 3.1415926535;`       |
| **Character** | `char`    | 2 bytes   | Stores a single Unicode character.      | `char grade = 'A';`               |
| **Boolean** | `boolean` | 1 bit     | Stores only `true` or `false` values.     | `boolean isLoggedIn = true;`      |

*Note: The `L` suffix for `long` and `f` for `float` are important to tell the compiler to treat the literal value as that specific type.*

---

### **4. Wrapper Types, Casting, and Autoboxing**

#### **Wrapper Types**
For every primitive type, Java provides a corresponding **class** called a Wrapper class. These classes "wrap" a primitive value inside an object.

*   **Why are they needed?** The Java Collections Framework (like `ArrayList`, `HashMap`) can only store objects, not primitives. Wrapper classes bridge this gap.
*   **Examples:** `int` → `Integer`, `double` → `Double`, `char` → `Character`, `boolean` → `Boolean`.

#### **Casting: Converting Between Types**
Casting is the process of converting a value from one data type to another.

*   **Widening Casting (Implicit/Automatic):** Converting a smaller type to a larger type size. This is safe and done automatically by Java.
    ```java
    int myInt = 100;
    double myDouble = myInt; // int is automatically widened to double
    System.out.println(myDouble); // Output: 100.0
    ```
*   **Narrowing Casting (Explicit/Manual):** Converting a larger type to a smaller type size. This is risky as it can lead to data loss. You must do it explicitly by putting the target type in parentheses.
    ```java
    double myDouble = 99.98;
    int myInt = (int) myDouble; // Manually cast double to int
    System.out.println(myInt); // Output: 99 (the .98 is lost)
    ```

#### **Autoboxing and Unboxing**
This is a convenience feature where Java automatically converts between primitive types and their corresponding Wrapper objects.

*   **Autoboxing:** Primitive → Wrapper Object.
    ```java
    Integer myInteger = 50; // Autoboxing: Java is secretly doing Integer.valueOf(50);
    ```
*   **Unboxing:** Wrapper Object → Primitive.
    ```java
    int myInt = myInteger; // Unboxing: Java is secretly doing myInteger.intValue();
    ```

---
```

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
 


---
---

## **End-to-End Study Guide: Inheritance in Java**

This module provides a detailed exploration of Inheritance, one of the four fundamental pillars of Object-Oriented Programming. We will cover the core concepts of superclasses and subclasses, the different types of inheritance, and how Java implements them.

### **Table of Contents**
1.  What is Inheritance? (The "Is-A" Relationship)
2.  Core Terminology: Superclass and Subclass
3.  The `extends` Keyword: How to Implement Inheritance
4.  Types of Inheritance (and Java's Implementation)
    *   Single Inheritance (Supported)
    *   Multilevel Inheritance (Supported)
    *   Hierarchical Inheritance (Supported)
    *   Multiple Inheritance (Not supported via classes, achieved via interfaces)
    *   Hybrid Inheritance (Not supported via classes, achieved via interfaces)
5.  The `super` Keyword: Accessing Parent Members
6.  Practice Worksheet & Solutions

---

### **1. What is Inheritance? (The "Is-A" Relationship)**

**Definition:** Inheritance is a fundamental mechanism in OOP that allows a new class to acquire, or **inherit**, the properties (fields) and behaviors (methods) of an existing class.

This creates a parent-child relationship between classes, formally known as a **superclass-subclass** relationship. The primary purpose of inheritance is **code reusability**. You can write common code once in a parent class and have it be automatically available to multiple child classes.

**The "Is-A" Test:**
The easiest way to know if inheritance is the right design choice is to use the "is-a" test. If you can say "Class B *is a* Class A," then Class B can inherit from Class A.
*   A `Car` **is a** `Vehicle`. (Correct)
*   A `Dog` **is an** `Animal`. (Correct)
*   An `Engine` **is a** `Car`. (Incorrect. An engine is *part of* a car. This is a "has-a" relationship, known as composition).

**Analogy: The Family Trait**
Think of inheritance like genetics in a family.
*   **Parents (Superclass):** Have general traits like having eyes, a nose, and the ability to breathe.
*   **Children (Subclass):** Automatically inherit these traits from their parents. They don't have to "re-invent" how to breathe. On top of these inherited traits, they can develop their own unique skills, like playing the guitar or speaking a different language.

---

### **2. Core Terminology: Superclass and Subclass**

*   **Superclass (Parent Class / Base Class):** The class whose features are inherited. It is the more general class. (e.g., `Vehicle`, `Animal`).
*   **Subclass (Child Class / Derived Class):** The class that inherits from another class. It is the more specialized class. It gets all the `public` and `protected` members of its superclass for free and can also add its own unique fields and methods. (e.g., `Car`, `Dog`).



---

### **3. The `extends` Keyword: How to Implement Inheritance**

In Java, you use the `extends` keyword to establish an inheritance relationship.

**Syntax:**
`class SubClassName extends SuperClassName { ... }`

**Program Example: The `Vehicle` and `Car` Hierarchy**
Let's build a simple hierarchy to demonstrate.

```java
// --- 1. The Superclass (Parent) ---
// It defines properties and methods common to ALL vehicles.
class Vehicle {
    String brand;
    protected int year; // protected is accessible by subclasses

    public void start() {
        System.out.println("Starting the vehicle's engine...");
    }

    public void stop() {
        System.out.println("Stopping the vehicle's engine.");
    }
}

// --- 2. The Subclass (Child) ---
// Car "is-a" Vehicle, so it extends it.
// It inherits 'brand', 'year', 'start()', and 'stop()'.
class Car extends Vehicle {
    // Car can also have its own specific fields and methods.
    int numberOfDoors;

    public void openTrunk() {
        System.out.println("The car's trunk is open.");
    }
    
    // It can also override a parent's method (Polymorphism)
    @Override
    public void start() {
        System.out.println("Starting the car with a key turn...");
    }
}

// --- 3. The Main Class for Testing ---
public class Main {
    public static void main(String[] args) {
        // Create an object of the subclass
        Car myCar = new Car();

        // --- Accessing inherited members from Vehicle ---
        myCar.brand = "Honda";
        myCar.year = 2023;
        System.out.println("My car is a " + myCar.year + " " + myCar.brand);
        
        // --- Accessing its own members ---
        myCar.numberOfDoors = 4;

        // --- Calling methods ---
        myCar.start();      // Calls the OVERRIDDEN method in Car
        myCar.openTrunk();  // Calls the method from Car
        myCar.stop();       // Calls the INHERITED method from Vehicle
    }
}
```

---

### **4. Types of Inheritance**

Java's implementation of inheritance is specific. Here's a breakdown of the common types and which ones Java supports directly with classes.

#### **a) Single Inheritance (Supported)**
A subclass inherits from only one superclass. This is the simplest and most common form of inheritance.
*   **Structure:** `A` ← `B`
*   **Example:** `class Car extends Vehicle {}` (This is what we've seen so far).

#### **b) Multilevel Inheritance (Supported)**
A class inherits from a subclass, creating a chain or a "grandparent-parent-child" relationship.
*   **Structure:** `A` ← `B` ← `C`
*   **Example:** `Vehicle` ← `Car` ← `ElectricCar`. The `ElectricCar` inherits from `Car`, which in turn inherits from `Vehicle`. `ElectricCar` gets the members of both `Car` and `Vehicle`.

**Program Example: Multilevel**
```java
class Animal { // Level 1
    void eat() { System.out.println("This animal eats food."); }
}

class Dog extends Animal { // Level 2
    void bark() { System.out.println("The dog barks."); }
}

class Puppy extends Dog { // Level 3
    void weep() { System.out.println("The puppy weeps."); }
}

public class Main {
    public static void main(String[] args) {
        Puppy myPuppy = new Puppy();
        myPuppy.eat();   // Inherited from Animal
        myPuppy.bark();  // Inherited from Dog
        myPuppy.weep();  // Its own method
    }
}
```

#### **c) Hierarchical Inheritance (Supported)**
One superclass is inherited by multiple subclasses.
*   **Structure:** `B` → `A` ← `C`
*   **Example:** `Car` extends `Vehicle`, and `Truck` also extends `Vehicle`. `Car` and `Truck` are siblings in the hierarchy.

**Program Example: Hierarchical**
```java
class Shape { // The single parent
    void draw() { System.out.println("Drawing a shape."); }
}

class Circle extends Shape { // Child 1
    void drawCircle() { System.out.println("Specifically, a circle."); }
}

class Square extends Shape { // Child 2
    void drawSquare() { System.out.println("Specifically, a square."); }
}

public class Main {
    public static void main(String[] args) {
        Circle c = new Circle();
        c.draw(); // Inherited
        c.drawCircle();

        Square s = new Square();
        s.draw(); // Inherited
        s.drawSquare();
    }
}
```

#### **d) Multiple Inheritance (NOT Supported via Classes)**
A single subclass tries to inherit from **two or more** superclasses.
*   **Structure:** `A` → `C` ← `B`
*   **Why it's not supported in Java:** It leads to the **"Diamond Problem."** Imagine `A` has a method `doSomething()`. Both `B` and `C` extend `A` and provide their own overridden versions of `doSomething()`. If `D` extends both `B` and `C`, which version of `doSomething()` should it inherit? This ambiguity is why Java's designers chose to avoid it for classes.
*   **Java's Solution:** A class can **implement multiple interfaces**. Since interfaces only provide method signatures (the "what," not the "how"), the subclass is simply forced to provide its own single implementation, avoiding the ambiguity. `class D implements B, C {}`.

#### **e) Hybrid Inheritance (NOT Supported via Classes)**
A combination of two or more types of inheritance (e.g., Hierarchical and Multiple). Since it involves Multiple Inheritance, it is also not supported directly via classes in Java but can be achieved through a combination of classes and interfaces.

---

### **5. The `super` Keyword: Accessing Parent Members**

The `super` keyword is a reference variable that is used to refer to the immediate parent class object.

**Primary Uses:**
1.  **To call the superclass's constructor:** `super()` is used to call the constructor of the parent class. It **must be the very first statement** in the subclass's constructor. If you don't explicitly call it, the compiler will implicitly insert a call to the parent's no-argument `super()` constructor.
2.  **To access a superclass's method:** `super.methodName()` is used when a subclass has overridden a method but still needs to call the parent's original version.
3.  **To access a superclass's field:** `super.fieldName` is used if a subclass has a field with the same name as a field in the superclass.

**Program Example: Using `super`**
```java
class Person {
    String name;

    public Person(String name) {
        this.name = name;
        System.out.println("Person constructor called.");
    }

    public void display() {
        System.out.println("Name: " + name);
    }
}

class Employee extends Person {
    int employeeId;

    public Employee(String name, int employeeId) {
        // 1. Calling the parent's constructor using super().
        // This MUST be the first line.
        super(name); 
        this.employeeId = employeeId;
        System.out.println("Employee constructor called.");
    }
    
    @Override
    public void display() {
        // 2. Calling the parent's display() method using super.
        super.display(); 
        System.out.println("Employee ID: " + employeeId);
    }
}

public class Main {
    public static void main(String[] args) {
        Employee emp = new Employee("Anjali", 101);
        emp.display();
    }
}
```
**Expected Output:**
```
Person constructor called.
Employee constructor called.
Name: Anjali
Employee ID: 101
```
---
---

### **4. A Deeper Look at Visibility: The `protected` Modifier**

While `public` members are visible to everyone and `private` members are visible only within the same class, `protected` offers a crucial middle ground specifically designed for inheritance. It allows a parent class to hide its implementation details from the outside world, yet still allow its children to access and extend that implementation.

**Definition:** A `protected` member (field or method) is accessible within:
1.  The same class where it is declared.
2.  Any other class within the **same package**.
3.  Any **subclass**, even if that subclass is in a different package. This is the key feature for inheritance.

**Analogy: A Family Secret Recipe**
This analogy helps clarify the different levels of access:
*   **`private` (Personal Diary):** Your personal, secret thoughts. No one else knows.
*   **`default` (Family Fridge Note):** A note on the family fridge. Anyone living in the house (same package) can see it, but guests from another house cannot.
*   **`protected` (Family Recipe Book):** A secret family recipe book. Anyone in the immediate family (same package) can use it. Additionally, if a child moves away (different package) but is still family (a subclass), they also get a copy of the recipe book. A complete stranger (an unrelated class in another package) would not have access.
*   **`public` (Published Blog Recipe):** A recipe published on a public blog. Everyone, everywhere, can see it.

**When to Use `protected`:**
Use `protected` for methods or fields that are not meant to be part of the public API of your class, but you anticipate that subclasses will need to access or override them to function correctly. For example, a `Vehicle` class might have a `protected void igniteSparkPlugs()` method. It's an internal process, but a specialized `PerformanceCar` subclass might need to override it to provide a more advanced ignition sequence.

**Program Example: Demonstrating `protected` Across Packages**

To see this in action, we must simulate having two different packages.

**File 1: `Vehicle.java` (in package `transport`)**
```java
// Save this file in a folder structure like: .../transport/Vehicle.java
package transport;

public class Vehicle {
    public String brand; // Public, visible everywhere

    // Protected: Visible to the 'transport' package and all subclasses of Vehicle.
    protected int year;
    
    // Protected method
    protected void startEngine() {
        System.out.println("Generic engine starting... (Protected Method in Vehicle)");
    }
}
```

**File 2: `Car.java` (in package `road`)**
This class is in a different package, but because it `extends Vehicle`, it gains access to the `protected` members.

```java
// Save this file in a folder structure like: .../road/Car.java
package road;

// We must import the Vehicle class from the other package.
import transport.Vehicle;

public class Car extends Vehicle {
    
    public void showDetails() {
        // --- Accessing inherited members from the parent ---
        
        // LEGAL: 'brand' is public.
        this.brand = "Toyota"; 
        
        // LEGAL: 'year' is protected, and Car IS-A subclass of Vehicle.
        this.year = 2023;
        
        System.out.println("Brand: " + this.brand);
        System.out.println("Year: " + this.year);
        
        // We can also call the protected method because Car is a subclass.
        this.startEngine();
    }
}
```
**File 3: `Boat.java` (in package `water`)**
This class is in a different package and is NOT a subclass, so it cannot access the `protected` members.
```java
// Save this file in a folder structure like: .../water/Boat.java
package water;
import transport.Vehicle;

public class Boat {
    public void tryToAccessVehicleMembers() {
        Vehicle v = new Vehicle();
        v.brand = "SomeBrand"; // LEGAL: 'brand' is public.
        
        // v.year = 2020; // COMPILE ERROR! 'year' has protected access in 'transport.Vehicle'.
                      // The Boat class is not in the same package and is not a subclass.
                      
        // v.startEngine(); // COMPILE ERROR for the same reason.
    }
}
```

---
---

### **6. The Constructor Chain: Calling Order and the `super` Keyword**

This is a critical, often-tested concept in inheritance that explains how objects are properly initialized.

#### **The Golden Rule of Constructor Chaining**

When an object of a subclass is created, the constructor of its **superclass is always called first**, before the constructor of the subclass. This process continues all the way up the inheritance hierarchy to the `Object` class (the ultimate ancestor of all classes in Java).

**Why?** This ensures that an object is built from the "inside out"—its most fundamental parts (from the superclass) are initialized before its more specialized parts (from the subclass) are added. A `Car` object cannot be properly initialized until the fundamental `Vehicle` part of it has been constructed.

#### **How it Works: The Implicit and Explicit `super()` Call**

The magic behind this chain is the `super()` keyword.

*   **Implicit Call:** If you do **not** write any `this()` or `super()` call as the first line of your constructor, the Java compiler **automatically inserts a call to `super()`**. This is a call to the **no-argument constructor** of the parent class.
*   **Explicit Call:** You can (and often must) call a specific parent constructor yourself using `super(arguments)`.

**Critical Rule:** A call to `this()` or `super()` **must be the very first statement** in a constructor. You cannot have any other code before it.

**The Common Pitfall:**
If the parent class does **not** have a no-argument constructor (e.g., it only has a constructor like `Parent(String name)`), then the implicit `super()` call in the child's constructor will fail. This will cause a **compile-time error**. In this situation, you are **forced** to explicitly call the available parameterized constructor from the child, like `super("some default name")`.

#### **Program Example: Tracing the Constructor Call Chain**

This example clearly demonstrates the order of execution.

```java
// Level 1: The Grandparent
class Grandparent {
    public Grandparent() {
        System.out.println("Step 1: Grandparent constructor is called.");
    }
}

// Level 2: The Parent
class Parent extends Grandparent {
    public Parent() {
        // The compiler implicitly inserts 'super();' here, calling the Grandparent constructor.
        System.out.println("Step 2: Parent constructor is called.");
    }
}

// Level 3: The Child
class Child extends Parent {
    public Child() {
        // The compiler implicitly inserts 'super();' here, calling the Parent constructor.
        System.out.println("Step 3: Child constructor is called.");
    }
}

public class Main {
    public static void main(String[] args) {
        System.out.println("Creating a Child object...");
        Child myChild = new Child();
        System.out.println("...Child object has been created!");
    }
}
```

**Expected Output:**
```
Creating a Child object...
Step 1: Grandparent constructor is called.
Step 2: Parent constructor is called.
Step 3: Child constructor is called.
...Child object has been created!
```
**Explanation of the Output:**
1.  When `new Child()` is called in `main`, the `Child` constructor is invoked.
2.  The `Child` constructor's first (implicit) action is to call `super()`, which is the `Parent()` constructor.
3.  The `Parent` constructor's first (implicit) action is to call `super()`, which is the `Grandparent()` constructor.
4.  The chain stops at the top. The `Grandparent` constructor runs fully and prints its message ("Step 1").
5.  Control returns to the `Parent` constructor, which now runs the rest of its body and prints its message ("Step 2").
6.  Finally, control returns to the `Child` constructor, which runs the rest of its body and prints its message ("Step 3").
---
---



### **7. Dynamic Method Dispatch: The Engine of Polymorphism**

**Dynamic Method Dispatch** is the mechanism that makes runtime polymorphism work in Java. It is the process by which a call to an overridden method is resolved at **runtime**, rather than at compile-time. This is why runtime polymorphism is also known as *dynamic binding*.

#### **How it Works**

When you have a superclass reference variable pointing to a subclass object, the compiler and the JVM perform different checks:

1.  **Compile-time Check:** The compiler only looks at the **reference type** (the superclass). It checks if the method you are calling *exists* in that superclass. If the method doesn't exist in the superclass, you will get a compile-time error, even if the method exists in the subclass object it's pointing to. The compiler's job is simply to say, "Yes, a `Vehicle` is capable of performing this action."

2.  **Runtime Check (The "Dispatch"):** At runtime, the Java Virtual Machine (JVM) looks at the **actual object** that the reference is pointing to. It checks if *that specific object's class* has an overridden version of the method.
    *   If **yes**, the JVM calls the **overridden method** from the subclass.
    *   If **no**, the JVM walks up the inheritance chain and calls the method from the **superclass**.

This runtime decision-making process is called Dynamic Method Dispatch.

**Analogy: A Universal Remote Control**
Imagine you have a universal remote control labeled "Entertainment Device" (the superclass reference, `Device`).
*   You can point this remote at a TV, a Blu-ray Player, or a Sound System (subclass objects).
*   When you press the "Power" button (call the `powerOn()` method), the compiler just checks, "Does an Entertainment Device have a Power button?" Yes, it does. So the code compiles.
*   At runtime, when you actually press the button, the remote sends a specific signal depending on what it's pointing at. If it's pointing at the **TV**, it sends the TV's power-on signal. If it's pointing at the **Sound System**, it sends the Sound System's unique power-on signal. The specific action is "dispatched" based on the actual object.

#### **Program Example: A Clear Demonstration**

Let's use a simple `Animal` hierarchy to see this in action.

```java
class Animal {
    public void speak() {
        System.out.println("The animal makes a generic sound.");
    }
}

class Dog extends Animal {
    @Override
    public void speak() {
        System.out.println("The dog barks: Woof! Woof!");
    }

    public void fetch() { // A method unique to Dog
        System.out.println("The dog is fetching a ball.");
    }
}

class Cat extends Animal {
    @Override
    public void speak() {
        System.out.println("The cat meows: Meow!");
    }
}

public class Main {
    public static void main(String[] args) {
        // 1. A superclass reference can hold a subclass object.
        Animal myPet; 

        // 2. Point the reference to a Dog object.
        myPet = new Dog();
        
        // DYNAMIC METHOD DISPATCH IN ACTION:
        // Compiler check: Does the 'Animal' class have a 'speak()' method? Yes. Code compiles.
        // Runtime check: What object is 'myPet' pointing to? A Dog.
        // JVM executes the Dog's overridden speak() method.
        myPet.speak(); // Output: The dog barks: Woof! Woof!

        // myPet.fetch(); // COMPILE ERROR! The compiler only sees the 'Animal' reference type,
                         // and the Animal class does not have a 'fetch()' method.

        // 3. Now, point the SAME reference to a Cat object.
        myPet = new Cat();

        // DYNAMIC METHOD DISPATCH AGAIN:
        // Compiler check: Does 'Animal' have 'speak()'? Yes.
        // Runtime check: What object is 'myPet' pointing to now? A Cat.
        // JVM executes the Cat's overridden speak() method.
        myPet.speak(); // Output: The cat meows: Meow!
    }
}
```

---
---

### **8. Using `final` with Inheritance: Setting Boundaries**

The `final` keyword is a non-access modifier that is used to apply restrictions. When used in the context of inheritance, it acts as a "stop sign," preventing further extension or modification down the hierarchy.

#### **1. `final` Methods**

When you declare a method as `final`, you are stating that this method's implementation is complete and **cannot be overridden** by any subclass.

*   **Syntax:** `public final void myCriticalMethod() { ... }`
*   **Why use it?**
    *   **Security:** To prevent subclasses from altering a core, security-sensitive behavior. For example, a method that validates a user's credentials might be made `final`.
    *   **To Guarantee Behavior:** To ensure that a specific method will always behave exactly as defined in the superclass, no matter what subclass is being used.

**Program Example:**

```java
class SuperClass {
    public void regularMethod() {
        System.out.println("This method can be overridden.");
    }

    // This method's implementation is now locked.
    public final void finalMethod() {
        System.out.println("This is a final method and cannot be changed.");
    }
}

class SubClass extends SuperClass {
    @Override
    public void regularMethod() {
        System.out.println("Subclass has overridden this method.");
    }

    /*
    @Override
    public void finalMethod() { // COMPILE ERROR!
        // error: finalMethod() in SubClass cannot override finalMethod() in SuperClass
        //        overridden method is final
        System.out.println("Trying to override...");
    }
    */
}

public class Main {
    public static void main(String[] args) {
        SubClass obj = new SubClass();
        obj.regularMethod(); // Calls the subclass's version
        obj.finalMethod();   // Calls the superclass's version (and cannot be changed)
    }
}
```

#### **2. `final` Classes**

When you declare an entire class as `final`, you are stating that this class is complete and **cannot be extended** (subclassed). It is at the very end of its inheritance line.

*   **Syntax:** `public final class MyFinalClass { ... }`
*   **Why use it?**
    *   **Immutability:** To create immutable classes. If a class is `final`, you can be certain that no subclass can be created to alter its state or behavior. The standard `String` and `Integer` classes in Java are `final` for this reason.
    *   **Security:** To prevent system classes from being extended in a way that could compromise the system.

**Program Example:**

```java
// This class is declared as final. No other class can inherit from it.
final class ImmutablePoint {
    private final int x;
    private final int y;

    public ImmutablePoint(int x, int y) {
        this.x = x;
        this.y = y;
    }

    public int getX() {
        return x;
    }
}

/*
// This will cause a COMPILE ERROR:
// error: cannot inherit from final ImmutablePoint
class SpecialPoint extends ImmutablePoint {
    // ...
}
*/

public class Main {
    public static void main(String[] args) {
        ImmutablePoint p = new ImmutablePoint(10, 20);
        System.out.println("Point created at x = " + p.getX());
    }
}
```

---
---

## **End-to-End Study Guide: Advanced OOP Concepts in Java**

This module delves into more advanced but essential Object-Oriented concepts. We will explore the different forms of Polymorphism in detail, understand the critical roles of `static` and `final` members, and uncover the power of Inner Classes.

### **Table of Contents**
1.  Polymorphism: The "Many Forms" Principle
    *   Method Overloading (Compile-time Polymorphism)
    *   Method Overriding (Runtime Polymorphism)
    *   Passing and Returning Objects from Methods
    *   Recursion: A Special Kind of Method Call
2.  Keywords for Control: `static` 
    *   Static Variables and Methods (Class Members)
3.  Nested and Inner Classes
    *   Inner Class (Non-static Nested Class)
    *   Static Nested Class
    *   Local and Anonymous Inner Classes
4.  Practice Questions & Solutions

---

### **1. Polymorphism: The "Many Forms" Principle**

Polymorphism is one of the four core pillars of OOP. The word means "many forms," and in programming, it translates to the ability of a single action or name to have different behaviors depending on the context. This principle allows for incredible flexibility and makes code easier to extend.

#### **1.1. Method Overloading (Compile-time / Static Polymorphism)**

**Definition:** Method overloading allows you to define **multiple methods with the same name** within the same class, as long as they have **different parameter lists**. The difference can be in:
1.  The **number** of parameters.
2.  The **type** of parameters.
3.  The **order** of parameter types.

The compiler determines which version of the method to call at **compile-time**, based on the arguments you provide. This is why it's also known as *static polymorphism*.

*   **Analogy:** Think of the `+` operator. It behaves differently based on its context.
    *   `5 + 10` performs **integer addition**.
    *   `"Hello" + " World"` performs **string concatenation**.
    The same operator (`+`) has different behaviors for different data types. Method overloading is you creating your own version of this for your methods.

**Program Example: A Flexible `Printer` Class**
```java
public class Printer {
    // 1. Overloading based on TYPE of parameter
    public void print(String message) {
        System.out.println("Printing a String: " + message);
    }

    public void print(int number) {
        System.out.println("Printing an Integer: " + number);
    }

    // 2. Overloading based on NUMBER of parameters
    public void print(String prefix, String message) {
        System.out.println(prefix + ": " + message);
    }

    // 3. Overloading based on ORDER of parameters
    public void print(String message, int repeatCount) {
        System.out.println("--- Repeating Message ---");
        for (int i = 0; i < repeatCount; i++) {
            System.out.println(message);
        }
    }

    public void print(int repeatCount, String message) {
        // Different order, different behavior
        System.out.println("--- Repeating Message (Order Swapped) ---");
        for (int i = 0; i < repeatCount; i++) {
            System.out.println((i + 1) + ". " + message);
        }
    }
}

public class Main {
    public static void main(String[] args) {
        Printer p = new Printer();
        p.print("Hello!");             // Calls the String version
        p.print(123);                  // Calls the int version
        p.print("LOG", "System OK");   // Calls the String, String version
        p.print("Repeat Me", 3);       // Calls the String, int version
        p.print(2, "Repeat Me Again"); // Calls the int, String version
    }
}
```

---
#### **1.2. Method Overriding (Runtime / Dynamic Polymorphism)**

This is the most powerful form of polymorphism and is intrinsically linked to **inheritance**.

**Definition:** Method overriding occurs when a **subclass provides a specific implementation** for a method that is already defined in its **superclass**. The method signature (name and parameters) in the subclass must be exactly the same as in the superclass.

When you call the overridden method on an object, the Java Virtual Machine (JVM) determines which version of the method to run (the parent's or the child's) at **runtime**, based on the **actual type of the object**, not the type of the reference variable.

*   **Analogy:** A "Speak" command.
    *   An `Animal` superclass has a generic `speak()` method that prints "An animal makes a sound."
    *   A `Dog` subclass **overrides** `speak()` to print "Woof!".
    *   A `Cat` subclass **overrides** `speak()` to print "Meow!".
    If you have a variable `Animal myPet = new Dog();`, calling `myPet.speak()` will execute the `Dog`'s version at runtime.

---

### **Complete Polymorphism Example: The Notification System (Single File)**

```java
// Main.java - All classes in one file for easy testing.

// --- 1. The Base Class (The "Superclass") ---
// Represents the general concept of a notification.
class Notification {
    // 'protected' means this field is accessible by this class and any subclasses.
    protected String recipient;

    public Notification(String recipient) {
        this.recipient = recipient;
    }

    // A generic method that provides default behavior.
    // Subclasses are expected to override this.
    public void send() {
        System.out.println("------------------------------------");
        System.out.println("Sending a GENERIC notification to " + recipient);
        System.out.println("------------------------------------");
    }
}


// --- 2. The Subclasses (Provide Specific Implementations) ---

// EmailNotification "is-a" Notification. It extends the base class.
class EmailNotification extends Notification {

    public EmailNotification(String emailAddress) {
        // 'super()' calls the constructor of the parent class (Notification)
        // to set the recipient field.
        super(emailAddress); 
    }

    // This method OVERRIDES the parent's send() method.
    // The @Override annotation is a good practice to ensure you are correctly overriding.
    @Override
    public void send() {
        System.out.println("------------------------------------");
        System.out.println("Sending Email Notification...");
        System.out.println("Recipient: " + this.recipient);
        System.out.println("Message: Your order has been shipped!");
        System.out.println("Email sent successfully.");
        System.out.println("------------------------------------");
    }
}

// SmsNotification "is-a" Notification.
class SmsNotification extends Notification {
    
    public SmsNotification(String phoneNumber) {
        super(phoneNumber);
    }

    // This method also OVERRIDES the parent's send() method with its own logic.
    @Override
    public void send() {
        System.out.println("------------------------------------");
        System.out.println("Sending SMS Notification...");
        System.out.println("To Phone: " + this.recipient);
        System.out.println("Msg: Your order has shipped!");
        System.out.println("SMS sent successfully.");
        System.out.println("------------------------------------");
    }
}


// --- 3. The Polymorphic Class ---
// This class contains a method that works with the base Notification type.
class NotificationSender {
    
    // This method demonstrates polymorphism.
    // It accepts ANY object that is a subclass of Notification.
    public void sendNotification(Notification notification) {
        // The magic happens here!
        // At runtime, Java checks the ACTUAL object type that 'notification'
        // is pointing to and calls the appropriate overridden 'send()' method.
        notification.send();
    }
}


// --- 4. The Main Class to Run the Demonstration ---
// The public class must match the filename (e.g., Main.java).
public class Main {

    public static void main(String[] args) {
        
        // Create an object that can send notifications.
        NotificationSender sender = new NotificationSender();

        // Create specific notification objects. Note that we are using the
        // parent class 'Notification' as the reference type. This is a common practice.
        Notification email = new EmailNotification("student@btech.edu");
        Notification sms = new SmsNotification("+91-9876543210");
        Notification generic = new Notification("some_user"); // An object of the parent class itself.

        System.out.println("### Dispatching All Notifications ###");

        // We pass different types of objects to the SAME method.
        // The method behaves differently depending on the object it receives.
        // This is polymorphism in action.
        
        sender.sendNotification(email);   // Will execute the code inside EmailNotification.send()
        sender.sendNotification(sms);     // Will execute the code inside SmsNotification.send()
        sender.sendNotification(generic); // Will execute the code inside the base Notification.send()
    }
}
```
### **Expected Output**
```
### Dispatching All Notifications ###
------------------------------------
Sending Email Notification...
Recipient: student@btech.edu
Message: Your order has been shipped!
Email sent successfully.
------------------------------------
------------------------------------
Sending SMS Notification...
To Phone: +91-9876543210
Msg: Your order has shipped!
SMS sent successfully.
------------------------------------
------------------------------------
Sending a GENERIC notification to some_user
------------------------------------
```
---
#### **1.3. Using Objects as Parameters and Return Types**

In Java, objects can be passed to and returned from methods just like primitive types. This is fundamental to building complex applications where objects need to interact.

**Program Example: A `Box` Factory**
This example shows a method that takes two `Box` objects as parameters and returns a new `Box` object that is a combination of the two.

---

### **Complete Example: Student Enrollment System (Single File)**

```java
// Main.java - All classes in one file for easy testing.

// --- 1. The Supporting Data Classes ---

// Represents a single student with basic details.
class Student {
    String studentId;
    String name;

    public Student(String studentId, String name) {
        this.studentId = studentId;
        this.name = name;
    }
}

// Represents a single course with a course code and title.
class Course {
    String courseCode;
    String title;

    public Course(String courseCode, String title) {
        this.courseCode = courseCode;
        this.title = title;
    }
}

// --- 2. The Result Class ---

// Represents the successful enrollment of a student in a course.
// This is the object that will be returned by our main method.
class Enrollment {
    // It holds references to the Student and Course objects it links together.
    Student student;
    Course course;
    java.util.Date enrollmentDate; // We can add extra info to the result object.

    public Enrollment(Student student, Course course) {
        this.student = student;
        this.course = course;
        this.enrollmentDate = new java.util.Date(); // Record the current date and time
    }

    // A method to display the details of this specific enrollment.
    public void displayConfirmation() {
        System.out.println("----- Enrollment Confirmation -----");
        System.out.println("Student ID:   " + student.studentId);
        System.out.println("Student Name: " + student.name);
        System.out.println("Course:       " + course.title + " (" + course.courseCode + ")");
        System.out.println("Date:         " + enrollmentDate);
        System.out.println("-----------------------------------");
    }
}

// --- 3. The Utility Class with the Core Logic ---

// This class contains the business logic for handling enrollments.
class EnrollmentSystem {

    // This method TAKES a Student object and a Course object as parameters.
    // It RETURNS a new Enrollment object.
    public Enrollment enrollStudent(Student studentToEnroll, Course courseToEnroll) {
        // In a real system, you would have more logic here:
        // - Check if the student is eligible for the course.
        // - Check if the course has available seats.
        // - Process payment, etc.
        
        System.out.println("\n>>> Processing enrollment for '" + studentToEnroll.name + "' in '" + courseToEnroll.title + "'...");

        // If all checks pass, create a new Enrollment object.
        Enrollment newEnrollment = new Enrollment(studentToEnroll, courseToEnroll);
        
        System.out.println("...Enrollment successful!");
        
        // Return the newly created confirmation object.
        return newEnrollment;
    }
}


// --- 4. The Main Class to Run the Demonstration ---
// The public class must match the filename (e.g., Main.java).
public class Main {

    public static void main(String[] args) {
        
        // --- Step 1: Create the initial data objects ---
        Student student1 = new Student("BTECH-CS-101", "Anjali Sharma");
        Course javaCourse = new Course("CS201", "Object-Oriented Programming with Java");
        
        // Create the system that will perform the action.
        EnrollmentSystem system = new EnrollmentSystem();
        
        // --- Step 2: Call the method, passing objects as arguments ---
        // The 'enrollmentConfirmation' variable will hold the object that is returned by the method.
        Enrollment enrollmentConfirmation1 = system.enrollStudent(student1, javaCourse);
        
        // --- Step 3: Use the returned object ---
        // We can now call methods on the object that was returned to us.
        // It's good practice to check if the returned object is not null.
        if (enrollmentConfirmation1 != null) {
            enrollmentConfirmation1.displayConfirmation();
        }

        // --- Let's do another example to show reusability ---
        Student student2 = new Student("BTECH-ME-102", "Vikram Singh");
        Course dbCourse = new Course("CS305", "Database Management Systems");

        Enrollment enrollmentConfirmation2 = system.enrollStudent(student2, dbCourse);
        if (enrollmentConfirmation2 != null) {
            enrollmentConfirmation2.displayConfirmation();
        }
    }
}
```

### **Expected Output**
(The exact date and time will vary)
```
>>> Processing enrollment for 'Anjali Sharma' in 'Object-Oriented Programming with Java'...
...Enrollment successful!
----- Enrollment Confirmation -----
Student ID:   BTECH-CS-101
Student Name: Anjali Sharma
Course:       Object-Oriented Programming with Java (CS201)
Date:         [Current Date and Time, e.g., Sat Nov 05 14:30:00 IST 2023]
-----------------------------------

>>> Processing enrollment for 'Vikram Singh' in 'Database Management Systems'...
...Enrollment successful!
----- Enrollment Confirmation -----
Student ID:   BTECH-ME-102
Student Name: Vikram Singh
Course:       Database Management Systems (CS305)
Date:         [Current Date and Time, e.g., Sat Nov 05 14:30:00 IST 2023]
-----------------------------------
```

---
#### **1.4. Recursion**

**Definition:** Recursion is a programming technique where a method calls itself to solve a problem. A recursive method breaks a problem down into smaller, identical subproblems until it reaches a simple case that can be solved directly.

Every recursive method must have two parts:
1.  **Base Case:** A condition that stops the recursion. Without it, the method would call itself forever, leading to a `StackOverflowError`.
2.  **Recursive Step:** The part where the method calls itself with a modified argument that moves it closer to the base case.

*   **Analogy:** A set of **Russian nesting dolls**. To find the smallest doll, you open the current doll (the recursive step), which reveals a slightly smaller doll. You repeat this process until you find the doll that doesn't open (the base case).

**Program Example: Factorial Calculation**
The factorial of a non-negative integer `n` is the product of all positive integers less than or equal to `n`. `n! = n * (n-1) * (n-2) * ... * 1`. This can be expressed recursively as `n! = n * (n-1)!`.

```java
public class RecursionExample {
    public static int factorial(int n) {
        // 1. Base Case: The condition that stops the recursion.
        if (n <= 1) {
            return 1;
        }
        // 2. Recursive Step: The method calls itself with a smaller problem.
        else {
            return n * factorial(n - 1);
        }
    }

    public static void main(String[] args) {
        int number = 5;
        int result = factorial(number);
        // How it works: 5 * factorial(4) -> 5 * 4 * factorial(3) -> ... -> 5 * 4 * 3 * 2 * 1
        System.out.println("The factorial of " + number + " is " + result); // Output: 120
    }
}
```

---

### **2. Keywords for Control: `static` 

#### **2.1. Static Members (Variables and Methods)**

**Definition:** The `static` keyword declares a member that belongs to the **class itself**, rather than to any individual object (instance) of the class.

*   **Static Variables:** Also known as class variables. There is only **one copy** of a static variable, which is shared among all objects of that class. If one object changes its value, the change is visible to all other objects.
    *   **Use Case:** A counter to track how many objects of a class have been created, or a constant that is common to all objects (like `Math.PI`).
*   **Static Methods:** Also known as class methods. They can be called directly on the class name without needing to create an object.
    *   **Key Restriction:** A static method **cannot** access non-static (instance) variables or methods directly, because there is no specific object instance (`this`) to work with.
    *   **Use Case:** Utility functions that don't depend on an object's state, like `Math.sqrt()` or `Integer.parseInt()`.

**Program Example: Tracking Student Enrollment**
```java
class Student {
    // Instance variable: Each student has their own name.
    String name;
    
    // Static variable: Shared by all Student objects.
    public static int studentCount = 0;

    public Student(String name) {
        this.name = name;
        studentCount++; // Increment the shared counter each time a new student is created.
    }
    
    // Static method: Belongs to the class.
    public static void displayTotalStudents() {
        System.out.println("Total students enrolled: " + studentCount);
    }
}

public class School {
    public static void main(String[] args) {
        // Call the static method directly on the class, before any objects exist.
        Student.displayTotalStudents(); // Output: 0

        System.out.println("Enrolling students...");
        Student s1 = new Student("Anjali");
        Student s2 = new Student("Vikram");

        // The studentCount has been updated by the constructors.
        System.out.println("s1's count is: " + s1.studentCount); // Accessing via instance (works, but not recommended)
        System.out.println("s2's count is: " + s2.studentCount);

        // The correct way to access a static member is via the class name.
        Student.displayTotalStudents(); // Output: 2
    }
}
```
---

### **3. Nested and Inner Classes**

Java allows you to define a class within another class. This is a powerful feature for logical grouping and enhanced encapsulation.

#### **3.1. Inner Class (Non-static Nested Class)**

**Definition:** An inner class is a non-`static` class that is defined inside another class. An object of an inner class can only exist *within* an instance of the outer class.

*   **Key Feature:** The inner class has **direct access to all members** (even `private` ones) of its enclosing outer class instance.
*   **Analogy:** A car's **engine**. The `Engine` is an inner class of the `Car` class. An `Engine` object cannot exist on its own; it's intrinsically part of a `Car` object and needs the car's state (like its fuel tank) to function.

**Program Example:**
```java
class Car {
    private String model;

    public Car(String model) { this.model = model; }

    // Inner Class definition
    class Engine {
        // This inner class method can access the private 'model' field of the outer Car.
        public void start() {
            System.out.println("Starting engine for the " + model);
        }
    }
    
    // A method in the outer class to start its engine
    public void startCar() {
        Engine engine = new Engine();
        engine.start();
    }
}

public class Main {
    public static void main(String[] args) {
        Car myCar = new Car("Tesla Model S");
        myCar.startCar(); // The common way to use an inner class
    }
}
```

#### **3.2. Static Nested Class**

**Definition:** A nested class that is declared with the `static` keyword.

*   **Key Feature:** It behaves like a regular top-level class that just happens to be "namespaced" inside another class for grouping. It **cannot** directly access the instance members of its outer class. It can only access `static` members of the outer class.
*   **Analogy:** A calculator's **`Memory` button**. The `Memory` is conceptually related to the `Calculator`, so you group it inside. But the `Memory` feature (`static class Memory`) can exist independently of any specific calculation happening on the calculator (`Calculator` object).

**Program 'Example:**
```java
class Outer {
    static int outerStaticVar = 10;
    int outerInstanceVar = 20;

    // Static Nested Class
    static class Nested {
        void show() {
            // Can access the static member of the outer class
            System.out.println("Outer static variable: " + outerStaticVar);
            
            // Cannot access instance member directly
            // System.out.println("Outer instance variable: " + outerInstanceVar); // ERROR!
        }
    }
}

public class Main {
    public static void main(String[] args) {
        // You can create an instance of the static nested class without an outer class instance.
        Outer.Nested nestedObject = new Outer.Nested();
        nestedObject.show();
    }
}
```

#### **3.3. Local and Anonymous Inner Classes**

These are more advanced and specialized forms of inner classes.

*   **Local Inner Class:** A class defined *inside a method*. Its scope is limited only to that method. It's used for very specific, localized tasks.
*   **Anonymous Inner Class:** An inner class with **no name**. It is declared and instantiated at the same time. It's a shorthand way to create a one-time-use object, typically for implementing an interface or extending a class with a small amount of override logic. This is very common in event handling in GUI programming.

**Program Example (Anonymous Inner Class):**
```java
interface Greeter {
    void greet();
}

public class Main {
    public static void main(String[] args) {
        // Here, we are creating an object of a class that has no name,
        // but it implements the Greeter interface.
        Greeter englishGreeter = new Greeter() {
            @Override
            public void greet() {
                System.out.println("Hello!");
            }
        };

        Greeter spanishGreeter = new Greeter() {
            @Override
            public void greet() {
                System.out.println("Hola!");
            }
        };

        englishGreeter.greet();
        spanishGreeter.greet();
    }
}
```

---
---

### **End-to-End Study Guide: Classes, Abstract Classes, and Interfaces**

This module introduces the core building blocks of Object-Oriented design in Java. We will start with the most fundamental unit—the **class**—and then explore its specialized forms: abstract classes and interfaces, which are the primary tools for achieving Abstraction.

### **Table of Contents**
1.  The Class: The Blueprint of OOP
2.  Abstract Classes: The Incomplete Blueprint
3.  Interfaces: The Pure Contract
4.  Key Differences: Abstract Class vs. Interface
5.  Practice Questions & Solutions

---

### **1. The Class: The Blueprint of OOP**

#### **1.1. Detailed Description: Classes and Objects**

In the real world, we are surrounded by objects: a car, a phone, a student, a bank account. Each of these objects has two key characteristics:
1.  **State:** The data or attributes that describe it (a car has a *color*, a *model*, and a *current speed*).
2.  **Behavior:** The actions it can perform (a car can *start*, *accelerate*, and *brake*).

In Object-Oriented Programming, a **class** is a blueprint or template that defines the common structure for a type of object. It specifies what attributes (state) its objects will have and what methods (behavior) they can perform.

An **object** (also called an **instance**) is a concrete entity created from that class blueprint. It exists in memory and has its own specific values for its attributes.

*   **Class:** The architectural blueprint for a house. It defines that a house will have rooms, doors, and windows.
*   **Object:** An actual, physical house built from that blueprint. Your house and your neighbor's house are two different objects built from the same blueprint; each has its own address and color.

#### **1.2. How to Define a Class in Java**

A class definition bundles fields (variables for state) and methods (functions for behavior).

> **Naming Convention:** Class names should always start with a capital letter and use `PascalCase` (e.g., `BankAccount`, `StudentDetails`).

**Program Example: The `Car` Class**
Let's build a simple `Car` class to model this.

```java
// File: Car.java
public class Car {
    // --- 1. Fields (Attributes) - Define the STATE of a Car ---
    // These are instance variables; each Car object gets its own copy.
    String model;
    String color;
    int year;
    double currentSpeed;

    // --- 2. Methods (Behaviors) - Define what a Car CAN DO ---
    // These methods will operate on the fields of a specific Car object.
    public void accelerate(double amount) {
        this.currentSpeed += amount;
        System.out.println("The " + this.color + " " + this.model + " is now moving at " + this.currentSpeed + " km/h.");
    }

    public void brake() {
        this.currentSpeed = 0;
        System.out.println("The " + this.model + " has stopped.");
    }

    public void displayDetails() {
        System.out.println("--- Car Details ---");
        System.out.println("Model: " + this.model);
        System.out.println("Color: " + this.color);
        System.out.println("Year: " + this.year);
        System.out.println("-------------------");
    }
}
```

#### **1.3. Creating and Using Objects**

Once you have the class (the blueprint), you can create objects (the actual cars) using the `new` keyword.

**The `new` keyword does three things:**
1.  **Allocates Memory:** It reserves space in the computer's heap memory for the new object.
2.  **Runs Constructor:** It calls the class's constructor to initialize the object's fields.
3.  **Returns a Reference:** It gives you back a memory address (a reference) that points to the new object.

**Program Example: The `Garage` (The Main Class)**

```java
// File: Garage.java
public class Garage {
    public static void main(String[] args) {
        // --- Creating Objects (Instances) of the Car class ---

        // 1. Declare a reference variable 'car1' of type Car.
        // 2. Use 'new Car()' to create a new Car object in memory.
        // 3. Assign the object's reference to the 'car1' variable.
        Car car1 = new Car();

        // --- Setting the STATE of the car1 object ---
        car1.model = "Honda Civic";
        car1.color = "Red";
        car1.year = 2022;

        // Create a second, completely separate Car object
        Car car2 = new Car();
        car2.model = "Ford Mustang";
        car2.color = "Black";
        car2.year = 2023;

        // --- Calling the BEHAVIORS (methods) on the objects ---
        System.out.println("Displaying initial car details:");
        car1.displayDetails();
        car2.displayDetails();

        System.out.println("\n--- Driving the cars ---");
        // This 'accelerate' call only affects the car1 object
        car1.accelerate(60);
        
        // This 'accelerate' call only affects the car2 object
        car2.accelerate(100);
        
        car1.brake();
    }
}
```
This fundamental concept of bundling data and methods into a single `class` is the foundation upon which all other OOP principles are built.

---

### **2. Abstract Classes: The Incomplete Blueprint**

Now that we understand a class is a blueprint, imagine a blueprint that is intentionally left incomplete. That's an **abstract class**.

#### **2.1. Detailed Description**

An abstract class is a special type of class that **cannot be used to create objects** (`new AbstractClass()` is illegal). It serves as a common base or template for a family of related classes that share some common code but must also provide their own unique implementation for certain features. It enforces an **"is-a"** relationship. A `Dog` *is an* `Animal`.

*   **When to use it?** When you have a group of related classes that share some common code, but each needs to behave differently in specific ways.
*   **Key Features:**
    *   Can have **concrete methods** (regular methods with a full implementation) to provide shared functionality to all its children.
    *   Can have **abstract methods** (methods with no body) to force its children to provide their own unique implementation for that behavior.
    *   Can have constructors, instance variables, and static methods, just like a regular class.

#### **2.2. The `abstract` Keyword**

*   To declare a class as abstract: `public abstract class ClassName`.
*   To declare a method as abstract: `public abstract returnType methodName();` (note the semicolon and lack of `{}`).

#### **2.3. Program Example: The `PaymentMethod` Hierarchy**
Imagine an e-commerce site that accepts payments via Credit Card, PayPal, and UPI. They all share the concept of an `amount` and a `validate()` step, but the actual processing is unique to each.

```java
// File: PaymentMethod.java
// This is an abstract blueprint for any payment method.
public abstract class PaymentMethod {
    protected double amount;

    public void setAmount(double amount) {
        this.amount = amount;
    }

    // A CONCRETE method: All subclasses inherit this exact implementation.
    public void validate() {
        System.out.println("Validating payment for amount: " + amount);
    }

    // An ABSTRACT method: There is no implementation here.
    // This forces any child class to provide its own version of this method.
    public abstract void processPayment();
}

// File: CreditCardPayment.java
// A concrete implementation of the abstract blueprint.
public class CreditCardPayment extends PaymentMethod {
    // We MUST provide an implementation for the abstract method.
    @Override
    public void processPayment() {
        System.out.println("Processing credit card payment of " + amount + "...");
        // Logic to connect to payment gateway, etc.
        System.out.println("Credit Card Payment Successful.");
    }
}

// File: UpiPayment.java
// Another concrete implementation.
public class UpiPayment extends PaymentMethod {
    @Override
    public void processPayment() {
        System.out.println("Processing UPI payment of " + amount + "...");
        // Logic to generate QR code or send to VPA.
        System.out.println("UPI Payment Successful.");
    }
}

// File: ECommerceSite.java (Main class)
public class ECommerceSite {
    public static void main(String[] args) {
        // We can't do this:
        // PaymentMethod pm = new PaymentMethod(); // ERROR! Cannot instantiate an abstract class.
        
        // We use polymorphism: A parent reference can hold a child object.
        PaymentMethod ccPayment = new CreditCardPayment();
        ccPayment.setAmount(1500.50);
        ccPayment.validate();       // Calling the shared concrete method from the parent.
        ccPayment.processPayment(); // Calling the child's specific implementation.

        System.out.println("---");

        PaymentMethod upiPayment = new UpiPayment();
        upiPayment.setAmount(499.00);
        upiPayment.validate();
        upiPayment.processPayment();
    }
}
```
---

### **3. Interfaces: The Pure Contract**

If an abstract class is an *incomplete blueprint*, an interface is a *pure contract* or a *list of rules*. It doesn't provide any blueprint at all; it just specifies what an object **must be able to do**.

#### **3.1. Detailed Description**

An interface defines a set of abstract methods. Any class that claims to **implement** this interface must provide a concrete implementation for **all** of its methods. It defines a **"can-do"** relationship or a capability.

*   **When to use it?** When you want to define a role or capability that can be shared by completely unrelated classes. For example, `Bird`, `Airplane`, and `Superhero` are unrelated, but they could all implement a `Flyable` interface.
*   **Key Features:**
    *   Traditionally, they only contained `public abstract` methods and `public static final` constants.
    *   They cannot be instantiated (`new MyInterface()` is illegal).
    *   They cannot have instance variables or constructors.
    *   A class can `implements` **multiple** interfaces, which is how Java achieves a form of multiple inheritance.

#### **3.2. The `interface` and `implements` Keywords**

*   To define an interface: `public interface InterfaceName`.
*   To make a class adhere to the contract: `public class MyClass implements InterfaceName, AnotherInterface`.

#### **3.3. Program Example: The `NotificationService` Contract**
A system needs to send notifications via various channels like Email, SMS, or Push Notification. The core application shouldn't care *how* the notification is sent, only *that* it can be sent.

```java
// File: NotificationService.java
// The contract: Any class that is a NotificationService MUST be able to send a notification.
public interface NotificationService {
    // Methods in an interface are 'public' and 'abstract' by default.
    void sendNotification(String recipient, String message);
}

// File: EmailService.java
// A class that promises to fulfill the NotificationService contract.
public class EmailService implements NotificationService {
    @Override
    public void sendNotification(String recipient, String message) {
        System.out.println("Sending EMAIL to " + recipient);
        System.out.println("Message: " + message);
        System.out.println("Email sent successfully.");
    }
}

// File: SmsService.java
// A completely different class that also fulfills the same contract.
public class SmsService implements NotificationService {
    @Override
    public void sendNotification(String recipient, String message) {
        System.out.println("Sending SMS to phone number: " + recipient);
        System.out.println("Message: " + message);
        System.out.println("SMS sent successfully.");
    }
}

// File: Application.java (Main class)
public class Application {
    // This method is powerful because it depends on the INTERFACE, not a concrete class.
    // It can accept ANY object, as long as that object implements NotificationService.
    public static void sendOrderConfirmation(NotificationService service, String customerContact) {
        System.out.println("\n--- Processing Order ---");
        // ... other order processing logic ...
        service.sendNotification(customerContact, "Your order #12345 has been confirmed.");
    }

    public static void main(String[] args) {
        // We can create objects of the concrete classes.
        NotificationService emailSender = new EmailService();
        NotificationService smsSender = new SmsService();

        // Now we can pass either object to the same method, and it just works.
        // This is the power of programming to an interface.
        sendOrderConfirmation(emailSender, "customer@example.com");
        sendOrderConfirmation(smsSender, "+91-9876543210");
    }
}
```

---

### **4. Key Differences: Abstract Class vs. Interface**

| Feature                 | Abstract Class                               | Interface                                         |
| :---------------------- | :------------------------------------------- | :------------------------------------------------ |
| **Purpose**             | To provide a common base for closely related classes (is-a). | To define a contract or capability for unrelated classes (can-do). |
| **Methods**             | Can have both **abstract and concrete** methods. | Traditionally, only `public abstract` methods. (Java 8+ allows `default` and `static` methods with bodies). |
| **Variables**           | Can have instance and static variables of any type. | Can only have `public static final` constants.     |
| **Inheritance**         | A class can `extends` only **one** abstract class. | A class can `implements` **multiple** interfaces. |
| **Constructor**         | **Has a constructor** (called by child constructors via `super()`). | **Does not have a constructor.**                     |

**When to Choose Which?**
*   Choose an **abstract class** when you want to create a hierarchy of components that are tightly related and share common code.
*   Choose an **interface** when you want to define a role or capability that different classes can perform, regardless of where they are in the inheritance hierarchy.

---
Of course. Based on the common patterns in academic exams, questions for this topic usually focus on definitions, differentiations, syntax, and applying the concepts to simple problems.

Here is a set of exam-style questions covering Classes, Abstract Classes, and Interfaces, complete with detailed answers.

---
---

## **Exam-Style Practice Questions: Classes, Abstract Classes & Interfaces**

### **Section A: Short Answer & Theory Questions (2-3 Marks Each)**

**Q1: What is a class in Java? Explain with a simple analogy.**

**Answer:**
A class in Java is a blueprint or template for creating objects. It defines a set of attributes (fields) and behaviors (methods) that the objects created from it will share. A class is a logical construct that does not occupy memory until an object is created from it.

**Analogy:** A class is like an architect's blueprint for a house. The blueprint itself is not a house, but it contains all the details (number of rooms, windows, etc.) needed to build multiple, physical houses (objects).

---

**Q2: Differentiate between a class and an object.**

**Answer:**

| Feature         | Class                                   | Object                                       |
| :-------------- | :-------------------------------------- | :------------------------------------------- |
| **Definition**  | A blueprint or template.                | An instance of a class.                      |
| **Nature**      | A logical entity.                       | A physical entity that exists in memory.   |
| **Memory**      | Does not occupy memory space.           | Occupies memory space in the heap.           |
| **Creation**    | Declared once using the `class` keyword. | Created many times using the `new` keyword. |
| **Example**     | The `Car` blueprint.                    | A specific red Honda Civic (`myCar`).      |

---

**Q3: What is a constructor? List two main rules for creating a constructor in Java.**

**Answer:**
A constructor is a special method in a class that is automatically called when an object of that class is created (using the `new` keyword). Its primary purpose is to initialize the object's instance variables to a valid starting state.

The two main rules for creating a constructor are:
1.  The constructor name must be **exactly the same** as the class name.
2.  A constructor **cannot have a return type**, not even `void`.

---

**Q4: Can an abstract class have a constructor? Justify your answer.**

**Answer:**
Yes, an abstract class can have a constructor.

**Justification:** Although you cannot create an object of an abstract class directly (e.g., `new MyAbstractClass()`), the abstract class still serves as a superclass for other concrete classes. When a subclass object is created, its constructor must call the superclass's constructor (either explicitly or implicitly via `super()`) as the first step in the constructor chain. Therefore, the abstract class needs a constructor to initialize its own fields that the subclass will inherit.

---

**Q5: What is an interface in Java? State its primary purpose.**

**Answer:**
An interface in Java is a purely abstract type that is used to specify a set of method signatures that a class must implement. It is a "contract" that defines a set of behaviors. An interface cannot be instantiated directly.

**Primary Purpose:** Its primary purpose is to achieve **100% abstraction** and to provide a mechanism for **multiple inheritance** in Java. It defines a "can-do" relationship, allowing completely unrelated classes to share a common capability.

---

### **Section B: Differentiation Questions (4-5 Marks Each)**

**Q6: Differentiate between an Abstract Class and an Interface. (Provide at least four key differences).**

**Answer:**

| Feature             | Abstract Class                                            | Interface                                                    |
| :------------------ | :-------------------------------------------------------- | :----------------------------------------------------------- |
| **Methods**         | Can have both **abstract** and **concrete** (implemented) methods. | Traditionally, only `public abstract` methods. (Java 8+ allows `default` and `static` methods with bodies). |
| **Variables**       | Can have instance variables, static variables, and constants. | Can only have `public static final` constants.             |
| **Inheritance**     | A class can `extends` only **one** abstract class.        | A class can `implements` **multiple** interfaces.          |
| **Constructor**     | **Has a constructor** to initialize its fields, called via `super()`. | **Does not have a constructor.**                             |
| **Purpose/Relationship** | To provide a common base for closely related classes (**is-a** relationship). | To define a contract or capability for unrelated classes (**can-do** relationship). |
| **Access Modifiers**  | Members can be `public`, `protected`, `default`, or `private`. | Methods are `public` by default.                           |

