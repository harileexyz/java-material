
---
---

## **End-to-End Study Guide: Polymorphism in Java**

This module provides a detailed exploration of Polymorphism, one of the four fundamental pillars of OOP. While Polymorphism literally means "many forms," in Java it refers to the ability of methods, variables, or objects to take on different behaviors or forms. We will cover the different types of polymorphism and related concepts like passing objects and recursion.

### **Table of Contents**
1.  **Method Overloading (Compile-time Polymorphism):** The Versatile Toolbox
2.  **Using Objects as Parameters:** Passing Blueprints as Input
3.  **Returning Objects from Methods:** Creating and Giving Back Blueprints
4.  **Recursion:** A Method Calling Itself

---

### **1. Method Overloading (Compile-time Polymorphism)**

#### **1.1. Detailed Description**

Method Overloading allows a single class to have **multiple methods with the same name**, as long as their **parameter lists are different**. The compiler determines which specific method to call at **compile-time**, based on the arguments provided in the method call. This is why it's also known as *static polymorphism* or *early binding*.

The parameter list can differ in three ways:
1.  **Number of parameters:** One method takes two arguments, another takes three.
2.  **Type of parameters:** One method takes an `int`, another takes a `double`.
3.  **Order of parameter types:** One method takes `(int, String)`, another takes `(String, int)`.

**Analogy to Remember: The Smartphone Calculator App**
*   Think of a calculator app. The `+` button (the method name) is always the same.
*   If you type `5 + 10`, it performs **integer addition**.
*   If you type `3.14 + 2.5`, it performs **floating-point addition**.
*   The same `+` operation (method name) behaves differently depending on the type of numbers (parameters) you give it. You are essentially creating your own custom version of this for your methods.

#### **1.2. Example: The `MathHelper` Analogy in Code**

Let's create a `MathHelper` class with an overloaded `add()` method.

```java
public class MathHelper {

    // Method 1: Adds two integers
    public int add(int a, int b) {
        System.out.println("-> Called the version that adds two integers.");
        return a + b;
    }

    // Method 2: Adds three integers (different NUMBER of parameters)
    public int add(int a, int b, int c) {
        System.out.println("-> Called the version that adds three integers.");
        return a + b + c;
    }
    
    // Method 3: Adds two doubles (different TYPE of parameters)
    public double add(double a, double b) {
        System.out.println("-> Called the version that adds two doubles.");
        return a + b;
    }
}

public class Main {
    public static void main(String[] args) {
        MathHelper helper = new MathHelper();
        
        // The compiler looks at the arguments to decide which 'add' method to call.
        
        System.out.println("Result: " + helper.add(5, 10));         // Calls Method 1
        System.out.println("Result: " + helper.add(5, 10, 20));     // Calls Method 2
        System.out.println("Result: " + helper.add(3.14, 2.71));    // Calls Method 3
    }
}
```

#### **1.3. Live Practice Question: The `Message` Broadcaster**

**Question:** Create a `Message` class with an overloaded `send()` method.
1.  Create a `send()` method that takes a `String` `textMessage` and prints "Sending text: [message]".
2.  Create a second `send()` method that takes a `String` `emailAddress` and a `String` `emailBody`, and prints "Sending email to [address] with body: [body]".
3.  In `main`, create a `Message` object and test both `send()` methods.

#### **Solution**
```java
class Message {
    // Version 1: For simple text messages
    public void send(String textMessage) {
        System.out.println("Sending text: '" + textMessage + "'");
    }
    
    // Version 2: For emails (overloaded with two String parameters)
    public void send(String emailAddress, String emailBody) {
        System.out.println("Sending email to " + emailAddress + " with body: '" + emailBody + "'");
    }
}

public class Main {
    public static void main(String[] args) {
        Message broadcaster = new Message();
        
        // Calling the first version of send()
        broadcaster.send("Meeting at 5 PM!");
        
        // Calling the second, overloaded version of send()
        broadcaster.send("student@btech.edu", "Your assignment is due tomorrow.");
    }
}
```

---

### **2. Using Objects as Parameters**

#### **2.1. Detailed Description**

Just as you can pass primitive types like `int` and `double` to methods, you can also pass objects. When you pass an object to a method, you are actually passing a **copy of the reference** (the memory address) to that object. This allows the method to access and interact with the original object's fields and methods. This is a fundamental concept for making objects interact with each other.

**Analogy to Remember: Giving a Friend the Key to Your House**
*   Your **house** is the **object** in memory.
*   Your **house key** is the **reference** to that object.
*   When you **give a copy of your key** (pass the reference) to a friend (a method), you are not giving them a new house. You are giving them access to your *one and only* house.
*   If your friend goes inside and paints the walls (modifies the object's state), the change is permanent. When you go home later, you will see the newly painted walls.

#### **2.2. Example: The `Car` and `Mechanic` Analogy in Code**

Let's model a `Mechanic` who performs a service on a `Car`. The `Car` object is passed to the `Mechanic`'s method.

```java
class Car {
    String model;
    int oilLevel; // Let's say 100 is full, 0 is empty

    public Car(String model) {
        this.model = model;
        this.oilLevel = 100; // New cars have full oil
    }

    public void displayStatus() {
        System.out.println("Car: " + model + ", Oil Level: " + oilLevel + "%");
    }
}

class Mechanic {
    // This method takes a Car object as a parameter (like giving the key to the mechanic).
    public void performOilChange(Car carToService) {
        System.out.println("Mechanic is servicing the " + carToService.model + "...");
        // The method modifies the state of the original Car object.
        carToService.oilLevel = 100;
        System.out.println("Oil change complete!");
    }
}

public class Main {
    public static void main(String[] args) {
        Car myCar = new Car("Honda Civic");
        Mechanic bob = new Mechanic();

        myCar.oilLevel = 20; // Let's say the oil is low
        System.out.println("--- Before Service ---");
        myCar.displayStatus();

        // Pass the 'myCar' object to the mechanic's method.
        bob.performOilChange(myCar);

        System.out.println("\n--- After Service ---");
        // The original myCar object has been modified.
        myCar.displayStatus();
    }
}
```

#### **2.3. Live Practice Question: `Student` and `Professor`**

**Question:** Create a system where a `Professor` can grade a `Student`'s assignment.
1.  Create a `Student` class with fields `name` and `grade` (char).
2.  Create a `Professor` class with a method `gradeAssignment(Student student)`.
3.  Inside this method, set the `grade` of the `student` object that was passed in to 'A'.
4.  In `main`, create a `Student` object (with an initial grade of 'F'), create a `Professor` object, and then pass the student to the professor's `gradeAssignment` method. Finally, print the student's grade again to show that it has been changed.

#### **Solution**
```java
class Student {
    String name;
    char grade;

    public Student(String name) {
        this.name = name;
        this.grade = 'F'; // Default grade
    }
}

class Professor {
    public void gradeAssignment(Student student) {
        System.out.println("Professor is grading " + student.name + "'s assignment...");
        student.grade = 'A';
    }
}

public class Main {
    public static void main(String[] args) {
        Student anjali = new Student("Anjali");
        Professor profSharma = new Professor();

        System.out.println(anjali.name + "'s initial grade: " + anjali.grade);

        // Pass the 'anjali' object to the professor
        profSharma.gradeAssignment(anjali);
        
        System.out.println(anjali.name + "'s final grade: " + anjali.grade);
    }
}
```

---

### **3. Returning Objects from Methods**

#### **3.1. Detailed Description**

Just as methods can accept objects as input, they can also **create and return objects as output**. This is an extremely common and powerful pattern used for creating objects that are the result of some calculation or process. The method acts as a "factory" that produces a new object.

**Analogy to Remember: The ATM Machine**
*   An **ATM** is the **method**.
*   You **insert your card and PIN** (the **parameters**).
*   The ATM performs a process (validates, checks balance).
*   It then **produces and returns a physical object**: a **receipt** (`Receipt` object).
*   You can then take this returned `Receipt` object and perform actions on it, like reading it (`receipt.read()`).

#### **3.2. Example: The `User` Factory Analogy in Code**

Let's create a `UserFactory` that takes raw data and returns a fully formed `User` object.

```java
// The object that will be returned
class User {
    String username;
    String email;

    public User(String username, String email) {
        this.username = username;
        this.email = email;
    }

    public void display() {
        System.out.println("User Profile -> Username: " + username + ", Email: " + email);
    }
}

// The factory class with a method that returns a User object
class UserFactory {
    // This method takes raw data and returns a new User object.
    public User createUser(String rawData) {
        // In a real app, this would be complex parsing logic.
        // Let's assume the data is "username,email".
        String[] parts = rawData.split(",");
        String username = parts[0];
        String email = parts[1];

        // Create and return the new object.
        User newUser = new User(username, email);
        return newUser;
    }
}

public class Main {
    public static void main(String[] args) {
        UserFactory factory = new UserFactory();
        
        String userDataFromDatabase = "Anjali,anjali@btech.edu";

        // Call the factory method and capture the returned User object.
        User user1 = factory.createUser(userDataFromDatabase);

        // Now we can use the object that the method gave back to us.
        user1.display();
    }
}
```

#### **3.3. Live Practice Question: The `Rectangle` Factory**

**Question:** Create a `Rectangle` factory.
1.  Create a `Rectangle` class with `width` and `height` fields, and a `displayArea()` method that prints the area.
2.  Create a `RectangleFactory` class with a method `createSquare(int sideLength)`.
3.  This method should create and **return a new `Rectangle` object** where both the width and height are equal to `sideLength`.
4.  In `main`, use the factory to create a square, capture the returned `Rectangle` object, and call its `displayArea()` method.

#### **Solution**
```java
class Rectangle {
    int width;
    int height;

    public Rectangle(int width, int height) {
        this.width = width;
        this.height = height;
    }

    public void displayArea() {
        System.out.println("The area is: " + (width * height));
    }
}

class RectangleFactory {
    // This method returns a Rectangle object
    public Rectangle createSquare(int sideLength) {
        // A square is just a special type of rectangle
        return new Rectangle(sideLength, sideLength);
    }
}

public class Main {
    public static void main(String[] args) {
        RectangleFactory factory = new RectangleFactory();
        
        System.out.println("Creating a square of side 10...");
        Rectangle mySquare = factory.createSquare(10);
        
        mySquare.displayArea();
    }
}
```

---

### **4. Recursion**

#### **4.1. Detailed Description**

**Recursion** is a programming technique where a method solves a problem by **calling itself**. To work correctly, a recursive method must break the problem down into smaller, identical subproblems until it reaches a simple "base case" that can be solved directly without further recursion.

Every recursive method must have two parts:
1.  **Base Case:** A condition that **stops** the recursion. Without it, you get a `StackOverflowError`.
2.  **Recursive Step:** The part where the method calls itself, but with an argument that moves it closer to the base case.

**Analogy to Remember: Russian Nesting Dolls**
*   Your task is to find the smallest, solid doll.
*   **Recursive Step:** You open the current doll. Inside, you find another, slightly smaller doll (an identical but smaller problem). You apply the same "open the doll" logic to this new doll.
*   **Base Case:** You eventually find a doll that doesn't open. This is the smallest one. You stop, and the task is complete.

#### **4.2. Example: The `Countdown` Analogy in Code**

```java
public class Countdown {

    public static void countdown(int number) {
        // 1. Base Case: If the number is zero or less, stop.
        if (number <= 0) {
            System.out.println("Liftoff!");
            return; // Stop the recursion
        }
        
        // Print the current number
        System.out.println(number);

        // 2. Recursive Step: Call the same method with a smaller number.
        countdown(number - 1);
    }

    public static void main(String[] args) {
        System.out.println("Starting recursive countdown from 5...");
        countdown(5);
    }
}
```
**Execution Trace:**
`countdown(5)` prints 5 and calls `countdown(4)`
`countdown(4)` prints 4 and calls `countdown(3)`
`countdown(3)` prints 3 and calls `countdown(2)`
`countdown(2)` prints 2 and calls `countdown(1)`
`countdown(1)` prints 1 and calls `countdown(0)`
`countdown(0)` hits the base case, prints "Liftoff!", and returns.

#### **4.3. Live Practice Question: Sum of Numbers**

**Question:** Write a recursive method `sumUpTo(int n)` that calculates the sum of all positive integers from 1 up to `n`.
*   For example, `sumUpTo(3)` should be `3 + 2 + 1 = 6`.
*   **Base Case:** If `n` is 1, the sum is 1.
*   **Recursive Step:** The sum up to `n` is `n` + the sum up to `n-1`.

#### **Solution**
```java
public class RecursiveSum {

    public static int sumUpTo(int n) {
        // Base Case: The simplest problem we can solve directly.
        if (n <= 1) {
            return 1;
        }
        
        // Recursive Step: Break the problem down.
        // The sum of numbers up to n is n + the sum of numbers up to (n-1).
        return n + sumUpTo(n - 1);
    }

    public static void main(String[] args) {
        int number = 5;
        int result = sumUpTo(number);
        // How it works: 5 + sum(4) -> 5 + (4 + sum(3)) -> 5 + 4 + 3 + 2 + 1
        System.out.println("The sum of numbers from 1 to " + number + " is: " + result); // Output: 15
    }
}
```