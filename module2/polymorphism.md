
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
2.  Keywords for Control: `static` and `final`
    *   Static Variables and Methods (Class Members)
    *   Final Variables, Methods, and Classes (Constants and Restrictions)
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

### **2. Keywords for Control: `static` and `final`**

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
#### **2.2. The `final` Keyword**

The `final` keyword is a non-access modifier used to apply restrictions. It can be applied to variables, methods, and classes.

*   **`final` Variables:** Creates a **constant**. Once a `final` variable has been assigned a value, it cannot be changed.
    *   **Convention:** `final` variable names are usually written in `ALL_CAPS`.
*   **`final` Methods:** A `final` method **cannot be overridden** by a subclass. This is used to ensure that a critical behavior in a superclass cannot be altered by its children.
*   **`final` Classes:** A `final` class **cannot be extended** (subclassed). This is done for security or to ensure the immutability of a class. The standard `String` class in Java is `final`.

**Program Example: A Configuration Class**
```java
// 1. A final class cannot be extended.
final class AppConfig {
    // 2. A final variable is a constant.
    public final int MAX_CONNECTIONS = 10;
    
    // 3. A final method cannot be overridden.
    public final void displayConfig() {
        System.out.println("Maximum Connections: " + MAX_CONNECTIONS);
    }
}

// class ExtendedConfig extends AppConfig { } // ERROR! Cannot inherit from final AppConfig.

public class Main {
    public static void main(String[] args) {
        AppConfig config = new AppConfig();
        // config.MAX_CONNECTIONS = 20; // ERROR! Cannot assign a value to a final variable.
        config.displayConfig();
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

## **✍️ Practice Questions**

### **Section A: Polymorphism**

**❓ Q1. Method Overloading: The `ShapeDrawer`**
Create a class called `ShapeDrawer`. In this class, create three overloaded methods named `draw()`:
1.  One that takes no arguments and prints "Drawing a generic shape."
2.  One that takes a `String` parameter `shapeColor` and prints "Drawing a shape with color: [color]".
3.  One that takes a `String` parameter `shapeName` and an `int` parameter `size`, and prints "Drawing a [shapeName] with size [size]."
Write a `main` method to test all three versions of the `draw()` method.

**❓ Q2. Method Overriding: The `Employee` Hierarchy**
1.  Create a base class `Employee` with a method `calculatePay()` that returns a `double` and simply returns `0.0`.
2.  Create two subclasses, `SalariedEmployee` and `HourlyEmployee`, that extend `Employee`.
    *   `SalariedEmployee` should have a `double` field for `monthlySalary`. Override `calculatePay()` to return this salary.
    *   `HourlyEmployee` should have fields for `hoursWorked` (double) and `hourlyRate` (double). Override `calculatePay()` to return `hoursWorked * hourlyRate`.
3.  In a `main` method, create one of each type of employee, store them in `Employee` reference variables, and print the calculated pay for each to demonstrate runtime polymorphism.

**❓ Q3. Object as Parameter/Return: The `Point` Class**
1.  Create a class `Point` with two `int` fields, `x` and `y`. Include a constructor to initialize them and a `display()` method to print their coordinates (e.g., "(x, y)").
2.  Create another class `GeometryUtils`. In this class, write a `static` method `findMidpoint(Point p1, Point p2)` that:
    *   Takes two `Point` objects as parameters.
    *   Calculates the midpoint coordinates: `midX = (p1.x + p2.x) / 2` and `midY = (p1.y + p2.y) / 2`.
    *   Creates and **returns a new `Point` object** representing this midpoint.
3.  In a `main` method, create two `Point` objects, call `findMidpoint()` to get the new midpoint object, and then call its `display()` method.

**❓ Q4. Recursion: Fibonacci Sequence**
Write a recursive method `fibonacci(int n)` that calculates the n-th number in the Fibonacci sequence. The sequence starts `0, 1, 1, 2, 3, 5, 8, ...`.
*   Base cases: `fibonacci(0)` is `0`, and `fibonacci(1)` is `1`.
*   Recursive step: `fibonacci(n) = fibonacci(n-1) + fibonacci(n-2)`.
Test it in a `main` method by calculating the 10th Fibonacci number.

---

### **Section B: `static`, `final`, and Inner Classes**

**❓ Q5. `static` and `final` in Action: The `Game` Class**
Create a class named `Game`.
1.  Add a `public static int` field named `gamesPlayed` to count the total number of games created. Initialize it to `0`.
2.  Add a `public final String` field named `GAME_TYPE` and initialize it to `"Adventure"`.
3.  In the constructor of the `Game` class, increment the `gamesPlayed` counter.
4.  Add a `static` method `getGamesPlayed()` that prints the current value of `gamesPlayed`.
5.  In a `main` method, create three `Game` objects. After creating them, call the `getGamesPlayed()` method to show the total count. Also, try to reassign a new value to `GAME_TYPE` to see the compiler error.

**❓ Q6. Inner Class: The `Computer` and `CPU`**
Create an outer class `Computer`.
1.  The `Computer` class should have a `private String` field `brand`.
2.  Inside the `Computer` class, create a non-static inner class named `CPU`.
3.  The `CPU` inner class should have a method `getBrandInfo()` that prints a message including the `brand` of the outer `Computer` (e.g., "This is a CPU for a [brand] computer.").
4.  In the `Computer` class, add a method `start()` that creates an instance of its `CPU` and calls the `getBrandInfo()` method.
5.  In a `main` method, create a `Computer` object and call its `start()` method.

---
---

## **✅ Solutions to Practice Questions**

### **Solution A1: Method Overloading: The `ShapeDrawer`**

```java
public class ShapeDrawer {

    // 1. No arguments
    public void draw() {
        System.out.println("Drawing a generic shape.");
    }

    // 2. Overloaded with a String parameter
    public void draw(String shapeColor) {
        System.out.println("Drawing a shape with color: " + shapeColor);
    }

    // 3. Overloaded with a String and an int
    public void draw(String shapeName, int size) {
        System.out.println("Drawing a " + shapeName + " with size " + size + ".");
    }

    public static void main(String[] args) {
        ShapeDrawer drawer = new ShapeDrawer();

        System.out.println("--- Calling the overloaded methods ---");
        drawer.draw();
        drawer.draw("Blue");
        drawer.draw("Triangle", 50);
    }
}
```

### **Solution A2: Method Overriding: The `Employee` Hierarchy**

```java
// Base class
class Employee {
    public double calculatePay() {
        // Base implementation, might represent a volunteer
        return 0.0;
    }
}

// Subclass 1
class SalariedEmployee extends Employee {
    private double monthlySalary;

    public SalariedEmployee(double salary) {
        this.monthlySalary = salary;
    }

    @Override
    public double calculatePay() {
        return this.monthlySalary;
    }
}

// Subclass 2
class HourlyEmployee extends Employee {
    private double hoursWorked;
    private double hourlyRate;

    public HourlyEmployee(double hours, double rate) {
        this.hoursWorked = hours;
        this.hourlyRate = rate;
    }

    @Override
    public double calculatePay() {
        return this.hoursWorked * this.hourlyRate;
    }
}

// Main class to test polymorphism
public class PayrollSystem {
    public static void main(String[] args) {
        // Using parent class references to hold child class objects
        Employee manager = new SalariedEmployee(50000.0);
        Employee consultant = new HourlyEmployee(40, 75.0);

        System.out.println("--- Calculating Pay ---");
        // At runtime, Java calls the correct overridden method based on the object's actual type.
        System.out.printf("Manager's Pay: ₹%.2f\n", manager.calculatePay());
        System.out.printf("Consultant's Pay: ₹%.2f\n", consultant.calculatePay());
    }
}
```

### **Solution A3: Object as Parameter/Return: The `Point` Class**

```java
// The Point class
class Point {
    int x;
    int y;

    public Point(int x, int y) {
        this.x = x;
        this.y = y;
    }

    public void display() {
        System.out.println("(" + this.x + ", " + this.y + ")");
    }
}

// The utility class
class GeometryUtils {
    public static Point findMidpoint(Point p1, Point p2) {
        int midX = (p1.x + p2.x) / 2;
        int midY = (p1.y + p2.y) / 2;

        // Create and return a new Point object
        return new Point(midX, midY);
    }
}

// Main class for testing
public class GeometryTest {
    public static void main(String[] args) {
        Point point1 = new Point(2, 4);
        Point point2 = new Point(10, 8);
        
        System.out.print("Point 1 is: ");
        point1.display();
        System.out.print("Point 2 is: ");
        point2.display();

        // Pass two Point objects and receive one Point object back
        Point midpoint = GeometryUtils.findMidpoint(point1, point2);

        System.out.print("The midpoint is: ");
        midpoint.display();
    }
}
```

### **Solution A4: Recursion: Fibonacci Sequence**

```java
public class FibonacciRecursive {

    public static int fibonacci(int n) {
        // Base Case 1: The start of the sequence
        if (n == 0) {
            return 0;
        }
        // Base Case 2: The second number in the sequence
        if (n == 1) {
            return 1;
        }
        // Recursive Step: Break the problem down
        return fibonacci(n - 1) + fibonacci(n - 2);
    }

    public static void main(String[] args) {
        int position = 10;
        int result = fibonacci(position);
        System.out.println("The Fibonacci number at position " + position + " is: " + result);
    }
}
```

### **Solution B5: `static` and `final` in Action: The `Game` Class**

```java
public class Game {
    // A static variable, shared across all Game objects
    public static int gamesPlayed = 0;

    // A final variable (constant), cannot be changed after initialization
    public final String GAME_TYPE = "Adventure";

    // The constructor increments the static counter
    public Game() {
        gamesPlayed++;
        System.out.println("A new game has started!");
    }

    // A static method to display the shared counter
    public static void getGamesPlayed() {
        System.out.println("Total games played so far: " + gamesPlayed);
    }
    
    public static void main(String[] args) {
        System.out.println("--- Welcome to the Game Arcade ---");
        
        Game.getGamesPlayed(); // Prints 0
        
        Game game1 = new Game();
        Game game2 = new Game();
        Game game3 = new Game();
        
        Game.getGamesPlayed(); // Prints 3
        
        // Let's try to change the final variable
        // game1.GAME_TYPE = "Action"; // This line would cause a COMPILE ERROR. Uncomment to see.
        System.out.println("The type of game1 is: " + game1.GAME_TYPE);
    }
}
```

### **Solution B6: Inner Class: The `Computer` and `CPU`**
```java
public class Computer {
    // Private field in the outer class
    private String brand;

    public Computer(String brand) {
        this.brand = brand;
    }

    // Non-static Inner Class
    class CPU {
        // This method can access the 'private' brand field of its enclosing Computer object.
        public void getBrandInfo() {
            System.out.println("This is a CPU for a " + brand + " computer.");
        }
    }

    // A method in the outer class to use the inner class
    public void start() {
        System.out.println("Starting the computer...");
        // Create an instance of the inner class
        CPU processor = new CPU();
        // Call the inner class's method
        processor.getBrandInfo();
    }

    public static void main(String[] args) {
        Computer myDell = new Computer("Dell");
        myDell.start();

        System.out.println();

        Computer myMac = new Computer("Apple");
        myMac.start();
    }
}
```