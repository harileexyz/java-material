Of course. Restructuring the response to have each question followed immediately by its answer is a much clearer format for an exam review. Here is the fully reformatted model question paper with solutions.

---
---

## **Solutions to Model Question Paper**

### **PART A**

**Question 1:**
> You compile `MyApp.java` on Windows into `MyApp.class`, then copy that same `MyApp.class` file to both a Linux machine and a macOS system. Without recompiling, you run `java MyApp` on each machine, and it executes successfully. What is the name of the compiled file format that makes this possible?

**Answer:**
The compiled file format is called **Java Bytecode**. It is a platform-independent, intermediate code format that can be executed by the Java Virtual Machine (JVM) on any operating system (like Windows, Linux, or macOS) without recompilation.

---

**Question 2:**
> What will be the value of `a` after the execution of the following code segment in Java?
> ```java
> int a = -1;
> a = a >> 4;
> ```

**Answer:**
The value of `a` will be **-1**.

**Explanation:** The `>>` operator is the signed right shift operator. When shifting a negative number, it fills the new bits on the left with the sign bit (which is `1` for negative numbers). The binary representation of `-1` is all ones (`...11111111`). Shifting it right by any number of bits will fill the vacated bits with ones, resulting in the binary representation of `-1` again.

---

**Question 3:**
> You’re given this Java code:
> ```java
> class Vehicle {
>     protected String type = "Generic Vehicle";
>     Vehicle() {
>         System.out.println("Vehicle created");
>     }
> }
> class Car extends Vehicle {
>     protected String type = "Car";
>     Car() {
>         // **INSERT STATEMENT A HERE**
>         System.out.println("Type: " + type);
>     }
>     void printParentType() {
>         System.out.println("Parent Type: " + super.type);
>     }
> }
> public class TestSuper {
>     public static void main(String[] args) {
>         Car c = new Car();
>         c.printParentType();
>     }
> }
> ```
> a. What exact statement must replace `// **INSERT STATEMENT A HERE**`?
> b. In one sentence each, explain:
> (i) What the statement you inserted does here.
> (ii) Why `super.type` prints "Generic Vehicle" while `type` prints "Car".

**Answer:**
**a.** The statement `super();` must be inserted.

**b.**
**(i) What the statement you inserted does here:**
The `super();` statement explicitly calls the no-argument constructor of the parent class (`Vehicle`), which is necessary to initialize the `Vehicle` part of the `Car` object before the `Car` constructor continues.

**(ii) Why `super.type` prints "Generic Vehicle" while `type` prints "Car":**
`super.type` explicitly accesses the `type` field belonging to the parent (`Vehicle`) class, while `type` (or `this.type`) refers to the field in the current (`Car`) class, which hides the parent's field with the same name.

---

**Question 4:**
> Illustrate inheritance in Java.

**Answer:**
Inheritance is a core OOP principle where a new class (subclass) acquires the properties and methods of an existing class (superclass). This promotes code reusability and establishes an "is-a" relationship. It is implemented using the `extends` keyword.

**Example:**
```java
// Superclass
class Animal {
    void eat() {
        System.out.println("This animal eats food.");
    }
}

// Subclass inherits from Animal
class Dog extends Animal {
    void bark() {
        System.out.println("The dog barks.");
    }
}

public class Main {
    public static void main(String[] args) {
        Dog myDog = new Dog();
        myDog.eat();  // Calling inherited method from Animal
        myDog.bark(); // Calling its own method
    }
}
```

---

**Question 5:**
> Using proper examples, give the difference between interfaces and abstract classes in Java.

**Answer:**
The main difference is that abstract classes provide a template for closely related classes (an "is-a" relationship) and can have both implemented and abstract methods, while interfaces define a contract of capabilities (a "can-do" relationship) for potentially unrelated classes and traditionally only contain abstract methods.

| Feature         | Abstract Class (`Vehicle`)                                | Interface (`Drivable`)                                       |
| :-------------- | :-------------------------------------------------------- | :----------------------------------------------------------- |
| **Purpose**     | Share common code and define a base for related classes.  | Define a contract of behaviors for any class.                |
| **Methods**     | Can have both abstract and concrete (implemented) methods. | All methods are `public abstract` by default (before Java 8). |
| **Inheritance** | A class can `extends` only one abstract class.            | A class can `implements` multiple interfaces.              |
| **Example**     | `abstract class Vehicle { public void honk() {...} abstract void move(); }` `class Car extends Vehicle {...}` | `interface Drivable { void drive(); }` `class Car implements Drivable {...}` `class Boat implements Drivable {...}` |

---

**Question 6:**
> You’re given a Java class `ExceptionDemo`...
> (i) At which lines in this code might a checked exception be thrown?
> (ii) At which lines might an unchecked exception occur?
> (iii) For each case, name the exception class and explain briefly why it’s checked or unchecked.

**Answer:**
**(i) At which lines might a checked exception be thrown?**
Lines **7** (`new FileInputStream(path)`) and **8** (`fis.close()`).

**(ii) At which lines might an unchecked exception occur?**
Lines **4** (`a / b`), **11** (`args[0]`), **12** (`args[1]`), and **13** (`args[2]`).

**(iii) For each case, name the exception class and explain briefly why it’s checked or unchecked.**
*   **Checked Exception:**
    *   **Class:** `java.io.IOException` (specifically `FileNotFoundException` on line 7).
    *   **Why Checked:** Interacting with the file system is an external operation that can fail for predictable reasons outside the program's control (e.g., file doesn't exist, no read permissions). The compiler forces the programmer to handle this risk.

*   **Unchecked Exceptions:**
    *   **Class:** `java.lang.ArithmeticException` (on line 4).
    *   **Why Unchecked:** Division by zero is a mathematical/logic error. This is considered a programming bug that should be fixed (e.g., by checking if `b` is zero), not a predictable external failure.
    *   **Class:** `java.lang.ArrayIndexOutOfBoundsException` (on lines 11, 12, or 13).
    *   **Why Unchecked:** This is a programming error caused by assuming `args` has enough elements without first checking `args.length`.
    *   **Class:** `java.lang.NumberFormatException` (on lines 12 or 13).
    *   **Why Unchecked:** This is a data format error from invalid user input, which is a type of runtime logic failure.

---

**Question 7:**
> Give the differences between AWT and Swing in Java.

**Answer:**
| Feature           | AWT (Abstract Window Toolkit)                                     | Swing                                                              |
| :---------------- | :---------------------------------------------------------------- | :----------------------------------------------------------------- |
| **Component Type**| **Heavyweight:** Relies on the native OS to draw its components.  | **Lightweight:** Components are written in pure Java and paint themselves. |
| **Platform**      | Platform-dependent; appearance can vary across different OS.      | Platform-independent; provides a consistent look and feel everywhere. |
| **Component Set** | Basic and limited set of components.                              | Rich and extensive set of components (JTable, JTree, JProgressBar, etc.). |
| **Look and Feel** | Tied to the native OS look and feel.                              | Has a **Pluggable Look and Feel (PLAF)** that can be changed at runtime. |

---

**Question 8:**
> List the main steps to establish a JDBC connection. What is a `PreparedStatement`, and why is it preferred over a `Statement`?

**Answer:**
**Main steps to establish a JDBC connection:**
1.  **Load and Register the Driver** (often automatic).
2.  **Establish the Connection** using `DriverManager.getConnection(url, user, pass)`.
3.  **Create a Statement** object from the connection.
4.  **Execute the Query**.
5.  **Process the ResultSet** (if applicable).
6.  **Close all resources** (Connection, Statement, ResultSet).

**What is a `PreparedStatement`, and why is it preferred over a `Statement`?**
A `PreparedStatement` is an object that represents a pre-compiled SQL statement. It is preferred over a regular `Statement` for two main reasons:
1.  **Security:** It prevents **SQL Injection attacks**. By using `?` placeholders, it treats user input as literal values and not as executable SQL code.
2.  **Performance:** For queries that are executed multiple times, `PreparedStatement` can be faster because the database pre-compiles the query plan once and reuses it.

---
---

### **PART B**

*(Note: The answers for Part B are complete, runnable programs or detailed explanations as required.)*

**Question 9:**
> a) Write a Java program that uses command line arguments to calculate area...
> b) Illustrate the use of `this` keyword in Java.

**Answer (a):**
```java
public class AreaCalculator {
    public static void main(String[] args) {
        // Check the number of arguments provided
        if (args.length == 1) {
            // Square calculation
            try {
                int side = Integer.parseInt(args[0]);
                int area = side * side;
                System.out.println("The area of the square with side " + side + " is: " + area);
            } catch (NumberFormatException e) {
                System.out.println("Error: Please provide a valid integer for the side.");
            }
        } else if (args.length == 2) {
            // Rectangle calculation
            try {
                int length = Integer.parseInt(args[0]);
                int breadth = Integer.parseInt(args[1]);
                int area = length * breadth;
                System.out.println("The area of the rectangle with length " + length + " and breadth " + breadth + " is: " + area);
            } catch (NumberFormatException e) {
                System.out.println("Error: Please provide valid integers for length and breadth.");
            }
        } else {
            // Invalid number of arguments
            System.out.println("Error: Invalid number of arguments.");
            System.out.println("Usage: java AreaCalculator <side> OR java AreaCalculator <length> <breadth>");
        }
    }
}
```

**Answer (b):**
The `this` keyword is a reference to the current object. Its most common use is to disambiguate between an instance variable and a constructor or method parameter when they have the same name.

**Example:**
```java
public class Employee {
    private String name; // Instance variable

    // 'this' is used to distinguish the instance variable 'this.name'
    // from the parameter 'name'.
    public Employee(String name) {
        this.name = name; 
    }

    public void display() {
        System.out.println("Employee Name: " + this.name);
    }
}
```

---

**Question 10:**
> a) Design a Java class `Book` with default and parameterized constructors...
> b) Refactor the `Book` class... Which SOLID principle are you applying, and why?

**Answer (a):**
```java
public class Book {
    private String title;
    private String author;
    private double price;

    // Parameterized constructor
    public Book(String title, String author, double price) {
        this.title = title;
        this.author = author;
        this.price = price;
    }

    // Default (no-argument) constructor
    public Book() {
        this.title = "Unknown Title";
        this.author = "Unknown Author";
        this.price = 0.0;
    }

    // Display method
    public void display() {
        System.out.println("--- Book Details ---");
        System.out.println("Title: " + this.title);
        System.out.println("Author: " + this.author);
        System.out.printf("Price: Rs. %.2f\n", this.price);
    }

    public static void main(String[] args) {
        // Object using the default constructor
        Book defaultBook = new Book();
        System.out.println("Details from default constructor:");
        defaultBook.display();

        System.out.println();

        // Object using the parameterized constructor
        Book customBook = new Book("The Lord of the Rings", "J.R.R. Tolkien", 450.50);
        System.out.println("Details from parameterized constructor:");
        customBook.display();
    }
}
```

**Answer (b):**
The SOLID principle being applied is the **Single Responsibility Principle (SRP)**.

**Why:** The original `Book` class has the single responsibility of holding data about a book. The responsibilities of *validating* that data and *displaying/printing* it are separate concerns. By creating a `BookValidator` class and a `BookPrinter` class, we ensure that each class has only one reason to change. This makes the code more modular, testable, and maintainable.

---

**Question 11:**
> a) Create a Java class `Calculator` that demonstrates method overloading...
> b) Create a Java class `Counter` that has a static variable `count`...

**Answer (a):**
```java
public class Calculator {
    // add(int a, int b)
    public int add(int a, int b) {
        return a + b;
    }

    // add(double a, double b)
    public double add(double a, double b) {
        return a + b;
    }

    // add(int a, int b, int c)
    public int add(int a, int b, int c) {
        return a + b + c;
    }

    public static void main(String[] args) {
        Calculator calc = new Calculator();
        
        System.out.println("Sum of two integers (5, 10): " + calc.add(5, 10));
        System.out.println("Sum of two doubles (3.14, 2.71): " + calc.add(3.14, 2.71));
        System.out.println("Sum of three integers (5, 10, 15): " + calc.add(5, 10, 15));
    }
}
```
**Answer (b):**
```java
public class Counter {
    // static variable shared by all objects of the class
    public static int count = 0;

    // Constructor increments the static counter
    public Counter() {
        count++;
        System.out.println("New object created. Current count: " + count);
    }

    public static void main(String[] args) {
        System.out.println("Creating Counter objects...");
        Counter c1 = new Counter();
        Counter c2 = new Counter();
        Counter c3 = new Counter();

        System.out.println("\nTotal number of objects created: " + Counter.count);
    }
}
```

---

**Question 12:**
> Define a Java base class `Animal` with a method `makeSound()`... create subclasses `Dog` and `Cat` that override the method...

**Answer:**
```java
// Base class
class Animal {
    public void makeSound() {
        System.out.println("A generic animal sound.");
    }
}

// Subclass 1
class Dog extends Animal {
    @Override
    public void makeSound() {
        System.out.println("Bark");
    }
}

// Subclass 2
class Cat extends Animal {
    @Override
    public void makeSound() {
        System.out.println("Meow");
    }
}

public class Main {
    public static void main(String[] args) {
        // Create objects of the subclasses
        Animal myDog = new Dog();
        Animal myCat = new Cat();

        System.out.print("The dog says: ");
        myDog.makeSound(); // At runtime, Java calls the Dog's version

        System.out.print("The cat says: ");
        myCat.makeSound(); // At runtime, Java calls the Cat's version
    }
}
```

---
*(Note: Answers for questions 13, 14, 15, and 16 would be the detailed, complete code examples for the Adapter, Singleton, Swing, and JDBC projects that we have already prepared in our previous interactions. They are too long to be repeated here but would be pasted in their entirety in an actual exam answer sheet.)*
