

## **End-to-End Study Guide: Introduction to Design Patterns in Java**

**Objective:** To introduce the concept of Design Patterns and provide a deep, practical understanding of two fundamental patterns: Singleton and Adapter.

### **Table of Contents**

1.  **What Are Design Patterns?** The Cooking Recipe Analogy
2.  **The Singleton Pattern:** Ensuring One and Only One
3.  **The Adapter Pattern:** Making Incompatible Things Work Together
4.  Practice Questions & Solutions

---
---

### **1. What Are Design Patterns?**

#### **1.1. Detailed Description**

A **Design Pattern** is a **general, reusable solution to a commonly occurring problem** within a given context in software design. It's not a finished piece of code that can be plugged in directly. Instead, it's a **template** or a **description** of how to solve a problem that can be used in many different situations.

Think of them as the collected wisdom of experienced software developers. Over decades, developers noticed they were solving the same kinds of problems over and over again. Design patterns are the documented, proven, and optimized solutions to these recurring problems.

**Why are they important?**
*   **Proven Solutions:** You don't have to reinvent the wheel. You are using a solution that has been tested and refined by many others.
*   **Shared Vocabulary:** When you say, "I'm using a Singleton for the database connection," other developers on your team immediately understand the structure and intent of your code without needing a lengthy explanation.
*   **Improved Code Structure:** Using patterns leads to code that is more maintainable, flexible, and reusable.

#### **1.2. Analogy to Remember: Cooking Recipes**

*   Imagine you want to make a cake. You could try mixing ingredients randomly, but you'll probably fail.
*   Instead, you look for a **recipe for "cake"**. A recipe is a **pattern**.
*   It gives you the **template**: a list of ingredients (components) and a set of instructions (the relationships between them).
*   It's **not a finished cake**. You still have to do the work, and you can adapt it (add chocolate chips, use a different pan), but the fundamental pattern for making a successful cake remains the same.
*   Similarly, there are recipes (patterns) for common software problems like "ensure only one object of a certain type ever exists" (Singleton) or "make two incompatible interfaces work together" (Adapter).

---
---

### **2. The Singleton Pattern**

**Category:** Creational Pattern (concerned with how objects are created).

#### **2.1. The Problem it Solves**

Sometimes, you need to ensure that there is **one, and only one, instance** of a particular class throughout your entire application.

**When would you need this?**
*   **Database Connections:** You typically want a single connection pool manager that all parts of your application share.
*   **Configuration Managers:** An application should have one central place to get configuration settings (like a `Configuration.getInstance()`).
*   **Logging Services:** You usually want a single logging object to handle all log messages to ensure they are written to a file in an orderly fashion.

Creating multiple instances of these would waste resources, lead to inconsistent behavior, and cause bugs.

#### **2.2. The Solution: How Singleton Works**

The Singleton pattern enforces the "one and only one" rule by making the class itself responsible for its own creation and lifecycle. It does this with three key ingredients:

1.  **A `private` static instance of itself:** The class holds its one and only instance in a `private static` field.
2.  **A `private` constructor:** This prevents anyone *outside* the class from creating a new instance using the `new` keyword.
3.  **A `public static` method (usually called `getInstance()`):** This is the single, global point of access. The first time this method is called, it creates the new instance. On every subsequent call, it simply **returns the already existing instance**.

#### **2.3. Analogy to Remember: The School Principal**

*   A school can have many teachers and many students, but there is **only one Principal**.
*   **Private Constructor:** You can't just "create" a new Principal. The position is controlled by the school's internal board.
*   **`getInstance()` Method:** If you need to speak to the Principal, you don't create one. You go to the front office and say, "I need to see the Principal." The office assistant (the `getInstance()` method) will then direct you to the **one and only** Principal that already exists. Everyone who asks gets directed to the same person.

#### **2.4. Example: A `DatabaseConnection` Singleton in Code**

Let's build a simple logger that ensures all parts of an application log to the same instance.

```java
public class Logger {
    // 1. A private static instance of the class itself.
    // It's initialized to null initially. This is called "lazy initialization".
    private static Logger instance;

    // A field to hold some data for our logger.
    private String logFile = "application.log";

    // 2. A private constructor. This prevents anyone from doing 'new Logger()'.
    private Logger() {
        // This could contain setup logic, like opening the log file.
        System.out.println("Logger instance created. Logging to: " + logFile);
    }

    // 3. The public static method to get the single instance.
    public static Logger getInstance() {
        // If an instance doesn't exist yet, create one.
        if (instance == null) {
            instance = new Logger();
        }
        // Return the one and only instance.
        return instance;
    }

    // A regular method for the logger to use.
    public void log(String message) {
        System.out.println("[LOG]: " + message);
    }
}

// Main class to demonstrate the Singleton pattern.
public class Main {
    public static void main(String[] args) {
        System.out.println("--- Starting Application ---");

        // Get the logger instance.
        Logger logger1 = Logger.getInstance();
        logger1.log("User logged in.");

        // Get the logger instance again from another part of the app.
        Logger logger2 = Logger.getInstance();
        logger2.log("Data was processed.");

        // --- Verification ---
        // Let's check if logger1 and logger2 are the same object.
        if (logger1 == logger2) {
            System.out.println("\nVerification: logger1 and logger2 are the exact same instance.");
            System.out.println("The Singleton pattern is working!");
        } else {
            System.out.println("\nError: Multiple logger instances were created.");
        }
    }
}
```
**Expected Output:**
```
--- Starting Application ---
Logger instance created. Logging to: application.log
[LOG]: User logged in.
[LOG]: Data was processed.

Verification: logger1 and logger2 are the exact same instance.
The Singleton pattern is working!
```
**Teaching Point:** Emphasize that "Logger instance created" is printed only **once**, even though we called `getInstance()` twice. This proves that the constructor was only run the first time.

---
---

### **3. The Adapter Pattern**

**Category:** Structural Pattern (concerned with how classes and objects are composed to form larger structures).

#### **3.1. The Problem it Solves**

You have two classes with **incompatible interfaces**, but you need them to work together. You cannot change the source code of one or both of these classes (perhaps they come from a third-party library).

**When would you need this?**
*   You have a new, modern charting library that expects data as a JSON object, but your old system provides data as an XML string.
*   Your application works with `Square` objects, but you are given a third-party library that provides `Rectangle` objects, and you need to make them fit.
*   You have a media player that understands `AudioPlayer` interfaces, but you are given a new video library with a `VideoPlayer` interface.

#### **3.2. The Solution: How Adapter Works**

The Adapter pattern acts as a **translator** or a **middleman**. You create a new class—the **Adapter**—that "wraps" one of the incompatible objects (the *adaptee*) and exposes an interface that the client code expects.

The Adapter's job is to receive calls in one format and translate them into calls in the format the adaptee understands.

#### **3.3. Analogy to Remember: The Power Plug Adapter**

*   **The Client:** Your Indian laptop with its three-pin plug.
*   **The Incompatible Service (Adaptee):** A two-pin American wall socket.
*   **The Problem:** Your laptop's plug doesn't fit into the American socket. Their interfaces are incompatible.
*   **The Solution (The Adapter):** You use a **power plug adapter**.
    *   One side of the adapter has the three-hole interface that your laptop **expects**.
    *   The other side has the two-pin plug that the American socket **provides**.
    *   The adapter's job is to simply translate between the two, allowing your laptop to get power from the wall socket.

#### **3.4. Example: The `Bird` and `ToyDuck` Analogy in Code**

Let's imagine we have a program that works with `Bird` objects, which can `fly()` and `makeSound()`. Now, we get a new class, `ToyDuck`, which can `squeak()`. We want to make the `ToyDuck` behave like a `Bird`.

```java
// --- Our system works with this interface ---
interface Bird {
    void fly();
    void makeSound();
}

// A concrete implementation of a bird
class Sparrow implements Bird {
    public void fly() {
        System.out.println("Sparrow is flying.");
    }
    public void makeSound() {
        System.out.println("Chirp chirp!");
    }
}


// --- The INCOMPATIBLE class from a third-party library ---
// We cannot change this class. It has a 'squeak' method, not 'makeSound'.
class ToyDuck {
    public void squeak() {
        System.out.println("Squeak squeak!");
    }
}


// --- The ADAPTER Class ---
// This class makes a ToyDuck look and behave like a Bird.
class BirdAdapter implements Bird {
    // The adapter holds a reference to the object it needs to adapt.
    private ToyDuck toyDuck;

    public BirdAdapter(ToyDuck toyDuck) {
        this.toyDuck = toyDuck;
    }

    // --- Translation Logic ---
    @Override
    public void fly() {
        // A toy duck can't fly, so we provide a sensible implementation.
        System.out.println("A toy duck can't fly.");
    }

    @Override
    public void makeSound() {
        // Here's the key translation: The 'makeSound' call is
        // translated into a 'squeak' call on the toy duck.
        toyDuck.squeak();
    }
}


// --- Main class to demonstrate ---
public class Main {
    public static void main(String[] args) {
        Sparrow sparrow = new Sparrow();
        ToyDuck plasticDuck = new ToyDuck();

        // Create an adapter to make the duck behave like a bird
        Bird duckAdapter = new BirdAdapter(plasticDuck);

        System.out.println("--- Testing the real bird ---");
        sparrow.fly();
        sparrow.makeSound();

        System.out.println("\n--- Testing the toy duck through the adapter ---");
        // We can now treat the adapted duck just like any other bird.
        duckAdapter.fly();
        duckAdapter.makeSound(); // This will call squeak() internally!
    }
}
```
**Expected Output:**
```
--- Testing the real bird ---
Sparrow is flying.
Chirp chirp!

--- Testing the toy duck through the adapter ---
A toy duck can't fly.
Squeak squeak!
```
**Teaching Point:** Emphasize that the `main` method works with `Bird` objects. It doesn't know or care that one of them is secretly a `ToyDuck` being translated by an adapter. This decoupling is the main benefit of the pattern.

---
---

## **Practice Questions & Solutions**

**❓ Q1. Singleton: The Game `Settings` Manager**
Create a Singleton class named `Settings`.
1.  The `Settings` class should have some configuration data, like `private String difficulty = "Normal";` and `private int volume = 75;`.
2.  Implement the Singleton pattern correctly (private constructor, private static instance, public static `getInstance()` method).
3.  Add public getter/setter methods for `difficulty` and `volume`.
4.  In `main`, get the `Settings` instance twice into two different variables (`settings1` and `settings2`).
5.  Use `settings1` to change the difficulty to "Hard".
6.  Then, use `settings2` to print the difficulty. If it prints "Hard", the Singleton is working.

**❓ Q2. Adapter: The `Image` Viewer**
You have an `ImageViewer` that can only `showPng(PngImage image)`. You are given a new library that provides `JpegImage` objects. Create an adapter.
1.  Create an interface `PngImage` with a method `render()`.
2.  Create a class `JpegImage` with a method `display()`.
3.  Create an `ImageAdapter` that implements `PngImage` but holds a `JpegImage`.
4.  The `render()` method of the adapter should call the `display()` method of the `JpegImage` it holds.
5.  Create an `ImageViewer` with a `showPng(PngImage image)` method.
6.  In `main`, create a `JpegImage` and an `ImageAdapter` for it, then pass the adapter to the `ImageViewer`.

---

## **✅ Solutions to Practice Questions**

**Solution Q1: The `Settings` Singleton**
```java
class Settings {
    private static Settings instance;
    private String difficulty = "Normal";
    private int volume = 75;

    private Settings() {} // Private constructor

    public static Settings getInstance() {
        if (instance == null) {
            instance = new Settings();
        }
        return instance;
    }

    // Getters and Setters
    public String getDifficulty() { return difficulty; }
    public void setDifficulty(String difficulty) { this.difficulty = difficulty; }
    public int getVolume() { return volume; }
    public void setVolume(int volume) { this.volume = volume; }
}

public class Main {
    public static void main(String[] args) {
        Settings settings1 = Settings.getInstance();
        Settings settings2 = Settings.getInstance();

        System.out.println("Initial difficulty: " + settings1.getDifficulty());

        // Change settings using the first reference
        System.out.println("Changing difficulty to 'Hard' using settings1...");
        settings1.setDifficulty("Hard");

        // Read settings using the second reference
        System.out.println("Difficulty according to settings2: " + settings2.getDifficulty());

        if (settings1 == settings2) {
            System.out.println("Verified: Both references point to the same object.");
        }
    }
}
```

**Solution Q2: The `Image` Adapter**
```java
// The interface our system expects
interface PngImage {
    void render();
}

// The incompatible class we are given
class JpegImage {
    private String imageName;
    public JpegImage(String name) { this.imageName = name; }
    public void display() {
        System.out.println("Displaying JPEG image: " + imageName);
    }
}

// The Adapter class
class ImageAdapter implements PngImage {
    private JpegImage jpegImage;

    public ImageAdapter(JpegImage jpegImage) {
        this.jpegImage = jpegImage;
    }

    // Translate the 'render' call to a 'display' call
    @Override
    public void render() {
        jpegImage.display();
    }
}

// Our client code that only understands PngImage
class ImageViewer {
    public void showPng(PngImage image) {
        System.out.print("ImageViewer is rendering the image... ");
        image.render();
    }
}

public class Main {
    public static void main(String[] args) {
        ImageViewer viewer = new ImageViewer();
        JpegImage jpeg = new JpegImage("vacation_photo.jpeg");

        // We can't pass 'jpeg' directly to the viewer.
        // viewer.showPng(jpeg); // COMPILE ERROR!

        // So we create an adapter that makes the JpegImage look like a PngImage.
        ImageAdapter adapter = new ImageAdapter(jpeg);

        // Now we can pass the adapter to the viewer.
        viewer.showPng(adapter);
    }
}
```

Of course. Focusing on just the Singleton pattern with targeted questions is a great way to ensure students master its intricacies.

Here are a variety of exam-style questions specifically for the Singleton Design Pattern, ranging from theory and definitions to code analysis and implementation.

---
---

### **Exam-Style Practice Questions: The Singleton Pattern**

### **Section A: Short Answer & Theory Questions (2-3 Marks Each)**

**Q1: What is the primary intent of the Singleton Design Pattern?**

**Answer:**
The primary intent of the Singleton Design Pattern is to **ensure that a class has only one instance** and to provide a **single, global point of access** to that instance.

---

**Q2: List the three essential components needed to correctly implement the Singleton pattern in Java.**

**Answer:**
1.  A **`private static` field** to hold the single instance of the class.
2.  A **`private` constructor** to prevent external instantiation with the `new` keyword.
3.  A **`public static` method** (commonly named `getInstance()`) that returns the single instance, creating it if it doesn't already exist.

---

**Q3: Give two real-world scenarios where using the Singleton pattern would be appropriate.**

**Answer:**
1.  **Configuration Manager:** An application needs a single object to manage and provide access to all its configuration settings (e.g., database URL, API keys, theme settings). Having multiple configuration objects could lead to inconsistent states.
2.  **Logging Service:** A system-wide logger that writes messages to a single file. If multiple logger objects existed, they might try to write to the same file simultaneously, causing file corruption or jumbled log messages.

---

**Q4: What is "lazy initialization" in the context of the Singleton pattern?**

**Answer:**
Lazy initialization is a strategy where the single instance of the Singleton class is not created until the `getInstance()` method is called for the first time. The instance is created "on-demand." This is achieved by checking if the static instance variable is `null` inside the `getInstance()` method. It is beneficial as it avoids creating the object if it is never used, saving memory and resources.

---

### **Section B: Code Analysis Questions (4-5 Marks Each)**

**Q5: The following code attempts to create a Singleton. Identify the flaw in the implementation. How would you fix it?**

```java
public class FlawedSingleton {
    public static FlawedSingleton instance = new FlawedSingleton();

    // The constructor is not private!
    public FlawedSingleton() {
        System.out.println("New instance created.");
    }
}

// In another file:
public class Main {
    public static void main(String[] args) {
        FlawedSingleton s1 = FlawedSingleton.instance;
        
        // The flaw is demonstrated here:
        FlawedSingleton s2 = new FlawedSingleton(); // This is possible!
        
        if (s1 == s2) {
            System.out.println("Singleton is working.");
        } else {
            System.out.println("Singleton is broken: multiple instances exist.");
        }
    }
}
```

**Answer:**

**The Flaw:** The constructor `public FlawedSingleton()` is declared as `public`. This allows any other class to create new instances of `FlawedSingleton` using the `new` keyword, which violates the core principle of the Singleton pattern.

**How to Fix It:** The constructor must be declared as **`private`**.

**Corrected Code Snippet:**
```java
public class FixedSingleton {
    public static FixedSingleton instance = new FixedSingleton();

    // FIX: Make the constructor private.
    private FixedSingleton() {
        System.out.println("New instance created.");
    }
}
```

---

**Q6: What will be the output of the following program? Explain your reasoning.**

```java
class President {
    private static President thePresident;

    private President() {
        System.out.println("A new president has been elected!");
    }

    public static President getInstance() {
        if (thePresident == null) {
            thePresident = new President();
        }
        return thePresident;
    }
}

public class Main {
    public static void main(String[] args) {
        System.out.println("First meeting:");
        President p1 = President.getInstance();

        System.out.println("Second meeting:");
        President p2 = President.getInstance();
    }
}
```

**Answer:**

**Output:**
```
First meeting:
A new president has been elected!
Second meeting:
```

**Explanation:**
1.  The `main` method starts, and "First meeting:" is printed.
2.  `President.getInstance()` is called for the first time.
3.  Inside `getInstance()`, the `if (thePresident == null)` check is performed. Since `thePresident` is `null` initially, the condition is true.
4.  The line `thePresident = new President();` is executed. This calls the `private` constructor, which prints "A new president has been elected!". The static `thePresident` variable now holds a reference to this new object.
5.  "Second meeting:" is printed.
6.  `President.getInstance()` is called for the second time.
7.  Inside `getInstance()`, the `if (thePresident == null)` check is performed again. This time, `thePresident` is **not null**, so the condition is false.
8.  The code inside the `if` block is skipped, and the existing instance is returned. The constructor is **not called a second time**. Therefore, no more text is printed.

---

### **Section C: Programming and Problem-Solving (5-10 Marks Each)**

**Q7: Implement a Singleton class named `GameManager`.**
The `GameManager` class should manage the state of a game.
1.  Implement the Singleton pattern correctly to ensure only one `GameManager` can exist.
2.  Add a `private` field `gameState` of type `String`, initialized to `"Not Started"`.
3.  Add two `public` methods:
    *   `startGame()` which changes the `gameState` to `"Running"`.
    *   `endGame()` which changes the `gameState` to `"Finished"`.
4.  Add a `public` method `displayGameState()` which prints the current `gameState`.
5.  In your `main` method, get the `GameManager` instance, start the game, display the state, end the game, and display the state again to prove it's managing a single, consistent state.

**Solution Q7:**
```java
class GameManager {
    private static GameManager instance;
    private String gameState;

    // Private constructor to prevent outside instantiation
    private GameManager() {
        this.gameState = "Not Started";
    }

    // Public static method to get the single instance
    public static GameManager getInstance() {
        if (instance == null) {
            instance = new GameManager();
        }
        return instance;
    }

    // Public methods to manage the game state
    public void startGame() {
        this.gameState = "Running";
        System.out.println("Game has started!");
    }

    public void endGame() {
        this.gameState = "Finished";
        System.out.println("Game has finished!");
    }
    
    public void displayGameState() {
        System.out.println("Current Game State: " + this.gameState);
    }
}

public class Main {
    public static void main(String[] args) {
        System.out.println("--- Accessing Game Manager ---");
        
        GameManager gm1 = GameManager.getInstance();
        gm1.displayGameState(); // Should print "Not Started"

        System.out.println("\n--- Starting the game ---");
        gm1.startGame();
        
        // Let's get the instance again from another part of the code
        GameManager gm2 = GameManager.getInstance();
        gm2.displayGameState(); // Should print "Running", because gm1 and gm2 are the same object

        System.out.println("\n--- Ending the game ---");
        gm2.endGame();
        gm1.displayGameState(); // Should print "Finished"
    }
}
```
---
---

## **End-to-End Study Guide: The SOLID Principles in Java**

**Objective:** To understand the five fundamental principles of Object-Oriented Design that lead to software that is easy to maintain, extend, and understand.

### **Introduction: What are SOLID Principles?**

SOLID is an acronym that represents five core design principles for writing clean, scalable, and maintainable Object-Oriented code. These principles were promoted by Robert C. Martin ("Uncle Bob") and are considered a cornerstone of modern software engineering.

**Analogy to Remember: The Rules of Good Architecture**
*   You can build a shack by randomly nailing boards together. It might stand for a while, but it will be unstable, hard to repair, and impossible to add a new room to.
*   An architect, however, follows fundamental principles: a solid foundation, load-bearing walls, proper plumbing and electrical plans. This results in a house that is stable, safe, and can be easily extended or renovated later.
*   **SOLID principles are the architectural rules for building good software.** Following them helps you avoid creating a "digital shack."

The five principles are:
1.  **S** - Single Responsibility Principle (SRP)
2.  **O** - Open/Closed Principle (OCP)
3.  **L** - Liskov Substitution Principle (LSP)
4.  **I** - Interface Segregation Principle (ISP)
5.  **D** - Dependency Inversion Principle (DIP)

---

### **1. S - Single Responsibility Principle (SRP)**

*   **The Rule:** A class should have **one, and only one, reason to change**.
*   **In Simple Terms:** Every class should have only **one job** or responsibility.
*   **Why?** If a class has multiple jobs, a change in one of those jobs can accidentally break the others. It also makes the class harder to understand and test.

*   **Analogy: The All-in-One Kitchen Gadget**
    *   **Bad (Violation):** A single gadget that is a blender, a toaster, a coffee maker, and a microwave. It has too many responsibilities. If the toaster heating element breaks, you have to send the *entire gadget* for repair, and you can't make coffee or blend a smoothie.
    *   **Good (Adherence):** Separate appliances: a blender, a toaster, a coffee maker. Each has a single job. If the toaster breaks, it doesn't affect your ability to make coffee.

#### **Example: The `Employee` Class**

**Bad (Violates SRP):** This class has three different responsibilities.
1.  Calculating pay (HR/Finance logic).
2.  Saving to the database (Database logic).
3.  Generating a report (Reporting logic).
A change in the database schema would force you to change this class. A change in the report format would also force you to change this class.

```java
// BAD: This class does too much.
class Employee {
    public void calculatePay() { /* ... */ }
    public void saveEmployeeToDatabase() { /* ... */ }
    public void generateReport() { /* ... */ }
}
```

**Good (Follows SRP):** We separate the responsibilities into different classes.
```java
// GOOD: Each class has only one job.

// Responsibility 1: Handle employee data.
class EmployeeData {
    private String name;
    private double salary;
    // Getters and setters...
}

// Responsibility 2: Handle payroll calculations.
class PayCalculator {
    public double calculatePay(EmployeeData employee) { /* ... */ return 0.0; }
}

// Responsibility 3: Handle database interactions.
class EmployeeRepository {
    public void save(EmployeeData employee) { /* ...logic to save to DB... */ }
}
```

#### **Practice Question (SRP)**

You have a `Book` class that holds the book's title and author. You are asked to add a feature to print the book's details. Which of the following two designs is better according to SRP, and why?

*   **Design A:** Add a `printBookDetails()` method directly inside the `Book` class.
*   **Design B:** Create a separate `BookPrinter` class with a method `print(Book book)`.

#### **Solution**
**Design B is better.**

**Reasoning:** The `Book` class's single responsibility is to hold data about a book. The responsibility of *printing* or *displaying* that data in a specific format (e.g., to the console, to a GUI, to a web page) is a separate concern. By creating a `BookPrinter` class, we follow SRP. If we later want to change how the book is printed (e.g., print to a file), we only need to change the `BookPrinter` class, not the `Book` class itself.

---

### **2. O - Open/Closed Principle (OCP)**

*   **The Rule:** Software entities should be **open for extension, but closed for modification**.
*   **In Simple Terms:** You should be able to add new functionality **without changing existing, working code**.
*   **Why?** Changing existing code is risky. It can introduce bugs into features that were already working perfectly.
*   **How?** Through abstraction (inheritance and interfaces).

*   **Analogy: A Laptop with USB Ports**
    *   **Closed for Modification:** You cannot (and should not) open your laptop's case and solder new connections directly onto the motherboard. The core design is "closed."
    *   **Open for Extension:** You can easily add new functionality by plugging in new devices (a mouse, a keyboard, an external hard drive) into the USB ports. The USB port is an abstraction that allows for extension.

#### **Example: The `AreaCalculator`**

**Bad (Violates OCP):** To add a new shape, we have to **modify** the `calculateArea` method. This is risky.
```java
// BAD: We have to change this class every time a new shape is added.
class AreaCalculator {
    public double calculateArea(Object shape) {
        if (shape instanceof Rectangle) {
            // ... calculate rectangle area
        }
        if (shape instanceof Circle) {
            // ... calculate circle area
        }
        // If we add a Triangle, we have to come back and add another 'if' statement here!
        return 0.0;
    }
}
```

**Good (Follows OCP):** We use an interface. The `AreaCalculator` is now closed for modification but open for extension.
```java
// GOOD: We program to an abstraction (interface).

interface Shape {
    double getArea();
}

class Rectangle implements Shape {
    public double getArea() { /* ... */ return 0.0; }
}

class Circle implements Shape {
    public double getArea() { /* ... */ return 0.0; }
}

// This class is now CLOSED for modification. It never needs to change.
class AreaCalculator {
    public double calculateArea(Shape shape) {
        return shape.getArea();
    }
}

// To add new functionality, we EXTEND by creating a new class. No existing code is touched.
class Triangle implements Shape {
    public double getArea() { /* ... */ return 0.0; }
}
```

#### **Practice Question (OCP)**

You have a `DiscountCalculator` class with a method `calculate(Customer customer)`. Inside, it has `if-else` statements to check the customer's type (`"Gold"`, `"Silver"`) to apply different discounts. How would you refactor this to follow the Open/Closed Principle, so you can add a `"Platinum"` customer type later without modifying the `DiscountCalculator`?

#### **Solution**
You would refactor it using an interface or an abstract class.

1.  Create an interface `Customer` with a method `double getDiscount()`.
2.  Create concrete classes `GoldCustomer`, `SilverCustomer`, etc., that `implement` the `Customer` interface and provide their specific discount logic in the `getDiscount()` method.
3.  The `DiscountCalculator` class's `calculate` method will now take a `Customer` interface as a parameter: `calculate(Customer customer)`. It will simply call `customer.getDiscount()`.
4.  To add a `PlatinumCustomer`, you just create a new class. The `DiscountCalculator` does not need to be changed.

---


---
---

### **A Deep Dive: The Liskov Substitution Principle (LSP)**

#### **1. The Formal Definition**

First, let's look at the formal definition by Barbara Liskov:
> "Let Φ(x) be a property provable about objects x of type T. Then Φ(y) should be true for objects y of type S where S is a subtype of T."

**Translation into Plain English:**
This definition is quite academic. In simpler programming terms, it means:

> **Objects of a superclass should be replaceable with objects of its subclasses without breaking the application.**

In other words, if you have a piece of code that works correctly with a `Parent` object, it must also work correctly and predictably with a `Child` object. The `Child` must be a perfect, "behaviorally compatible" substitute for the `Parent`.

#### **2. The Core Idea: The "Behavioral" Contract**

Inheritance is often taught as an "is-a" relationship, which is a great start. A `Square` *is a* `Rectangle`. A `Penguin` *is a* `Bird`. This is structurally true. However, LSP goes a step further and says that inheritance must also be about **behavioral subtyping**.

The subclass must not just inherit the methods of the parent; it must **honor the contract and behavior** of those methods. It can *extend* the behavior (add more functionality), but it cannot *violate* the parent's core assumptions or produce unexpected side effects.

**What does the "contract" include?**
*   **Method Signatures:** The child method must have the same name and parameters.
*   **Return Types:** The child method's return type must be the same as or a subtype of the parent's return type.
*   **Exceptions:** The child method should not throw new checked exceptions that the parent method does not declare.
*   **Preconditions (what must be true *before* the method runs):** The child method cannot strengthen the preconditions. It must accept at least everything the parent method accepts.
*   **Postconditions (what must be true *after* the method runs):** The child method cannot weaken the postconditions. It must deliver at least what the parent promises to deliver.

The last two points are the most subtle and are where most LSP violations occur.

#### **3. Analogy: The Substitute Teacher**

Let's use a clear, real-world analogy to understand this.

*   **The Superclass:** Your regular Math teacher, **Mr. Sharma**. The school (your program) has a contract with him.
    *   **Contract/Behavior:** When you ask Mr. Sharma a math question (`askQuestion()`), he will provide a correct mathematical answer. He will not sing a song or assign English homework.
*   **The Subclass:** A substitute teacher, **Ms. Davis**. She is also a `Teacher`, so she seems like a valid substitute.

*   **Scenario 1: LSP is Followed**
    *   Ms. Davis is also a qualified math teacher. When students ask her a math question (`askQuestion()`), she provides a correct mathematical answer, just like Mr. Sharma. Her teaching style might be slightly different (extending the behavior), but she fulfills the core contract.
    *   **Result:** The classroom continues to function correctly. Ms. Davis is a valid substitute for Mr. Sharma.

*   **Scenario 2: LSP is Violated**
    *   Ms. Davis is actually a history teacher who was assigned to the math class by mistake.
    *   When students ask her a math question (`askQuestion()`), she gets confused and either:
        1.  Gives a wrong answer.
        2.  Throws an "exception" by saying, "I can't answer that, I'm a history teacher!" and refuses to proceed.
        3.  Changes the subject entirely and starts talking about historical events (an unexpected side effect).
    *   **Result:** The classroom breaks down. The students get confused, and the learning process fails. Ms. Davis is **not a valid substitute** for Mr. Sharma because she violates the behavioral contract of a "Math Teacher".

**Key Takeaway:** Just because something structurally fits the "is-a" relationship doesn't mean it's a correct substitute behaviorally.

---

#### **4. The Classic Code Example: Rectangle vs. Square**

This is the most famous example used to demonstrate an LSP violation. It highlights how a seemingly logical inheritance structure can be behaviorally incorrect.

**The Setup:**
Mathematically, a square *is a* rectangle. So, let's model this with inheritance.

```java
// The Superclass
class Rectangle {
    protected int width;
    protected int height;

    public void setWidth(int width) {
        this.width = width;
    }

    public void setHeight(int height) {
        this.height = height;
    }

    public int getWidth() {
        return width;
    }

    public int getHeight() {
        return height;
    }

    public int getArea() {
        return this.width * this.height;
    }
}
```
**The `Rectangle`'s Behavioral Contract:**
The `Rectangle` class has an implicit behavioral contract:
1.  Setting the width **only** affects the width.
2.  Setting the height **only** affects the height.

**The Subclass (The LSP Violator):**
Now let's create a `Square` subclass. To maintain the property of a square (where width always equals height), we must override the setters.

```java
class Square extends Rectangle {
    @Override
    public void setWidth(int width) {
        // To maintain the square's integrity, we must change both sides.
        this.width = width;
        this.height = width;
    }

    @Override
    public void setHeight(int height) {
        // To maintain the square's integrity, we must change both sides.
        this.width = height;
        this.height = height;
    }
}
```
Here, the `Square` class **violates the behavioral contract** of the `Rectangle`. Setting the width now has an unexpected side effect: it also changes the height.

**The Client Code That Breaks:**
Now, let's write a piece of code (a "client") that works perfectly fine with a `Rectangle` but breaks when we substitute a `Square`.

```java
public class AreaCalculator {
    
    // This method has an expectation based on the Rectangle's behavior.
    public static void testArea(Rectangle r) {
        System.out.println("--- Testing a new shape ---");
        r.setWidth(5);
        r.setHeight(4);
        
        // The core assumption: The area should be width * height = 5 * 4 = 20.
        int expectedArea = 20;
        int actualArea = r.getArea();
        
        System.out.println("Expected Area: " + expectedArea);
        System.out.println("Actual Area: " + actualArea);
        
        if (expectedArea == actualArea) {
            System.out.println("Test Passed! The object behaves like a Rectangle.");
        } else {
            System.out.println("Test FAILED! This object does NOT behave like a Rectangle.");
        }
    }

    public static void main(String[] args) {
        Rectangle rect = new Rectangle();
        testArea(rect); // This will pass.

        Square square = new Square();
        testArea(square); // This will fail! We have substituted a child for a parent, and it broke the program.
    }
}
```

**Trace of the `testArea(square)` call:**
1.  `r.setWidth(5);` -> The `Square`'s override is called. `width` becomes 5, and `height` also becomes 5.
2.  `r.setHeight(4);` -> The `Square`'s override is called. `height` becomes 4, and `width` also becomes 4.
3.  `r.getArea()` is called. It calculates `width * height`, which is now `4 * 4 = 16`.
4.  The `actualArea` is 16, which does not equal the `expectedArea` of 20. The test fails.

**Conclusion:** The `Square` object is not a valid substitute for a `Rectangle` object because it changes the fundamental behavior expected by the client code. This is a clear violation of LSP.

#### **5. How to Fix an LSP Violation**

The solution is often to rethink the inheritance hierarchy.
*   Don't force an "is-a" relationship where the behaviors don't match.
*   Create a more generic base class or interface.

### **LSP-Compliant Design: `Shape` Hierarchy (Complete Code)**

This example is structured in a single file to be easily compiled and run in any Java environment, including online compilers.

```java
// Main.java - All classes in one file for easy testing.

// --- 1. The Abstraction: A Common Contract for All Shapes ---
// This interface defines the "contract" that all shapes must follow.
// In this case, every shape must be able to calculate its area.
interface Shape {
    double getArea();
}


// --- 2. Concrete Implementation 1: The Rectangle Class ---
// A Rectangle implements the Shape contract.
class Rectangle implements Shape {
    // A rectangle has its own distinct properties.
    protected int width;
    protected int height;

    public void setWidth(int width) {
        this.width = width;
    }

    public void setHeight(int height) {
        this.height = height;
    }

    // Fulfilling the contract by providing an implementation for getArea().
    @Override
    public double getArea() {
        return this.width * this.height;
    }
}


// --- 3. Concrete Implementation 2: The Square Class ---
// A Square ALSO implements the Shape contract. It does NOT extend Rectangle.
// It is treated as its own distinct type of shape.
class Square implements Shape {
    // A square has its own property: a single side length.
    protected int side;

    public void setSide(int side) {
        this.side = side;
    }

    // Fulfilling the contract by providing its own implementation for getArea().
    @Override
    public double getArea() {
        return this.side * this.side;
    }
}


// --- 4. The Main Class to Demonstrate the Correct Design ---
public class Main {

    public static void main(String[] args) {
        
        // --- Working with a Rectangle ---
        System.out.println("--- Testing a Rectangle ---");
        Rectangle rect = new Rectangle();
        rect.setWidth(5);
        rect.setHeight(4);
        System.out.println("Rectangle Area: " + rect.getArea()); // Expected: 20.0

        // --- Working with a Square ---
        System.out.println("\n--- Testing a Square ---");
        Square square = new Square();
        square.setSide(5);
        System.out.println("Square Area: " + square.getArea()); // Expected: 25.0

        // --- Polymorphism with the Interface ---
        // We can use the 'Shape' interface to refer to both objects.
        // This is useful for creating collections or methods that work with any shape.
        System.out.println("\n--- Demonstrating Polymorphism ---");
        
        Shape shape1 = new Rectangle();
        // We must cast it back to a Rectangle to access Rectangle-specific methods
        ((Rectangle) shape1).setWidth(10);
        ((Rectangle) shape1).setHeight(5);

        Shape shape2 = new Square();
        // We cast it back to a Square to access its specific setSide method
        ((Square) shape2).setSide(7);

        printShapeArea(shape1); // Passes a Rectangle object
        printShapeArea(shape2); // Passes a Square object
    }

    // A method that works with ANY object that implements the Shape interface.
    public static void printShapeArea(Shape shape) {
        // This method doesn't need to know if it's a Rectangle or a Square.
        // It only knows it's a Shape and can therefore call getArea().
        System.out.println("The area of the shape is: " + shape.getArea());
    }
}
```

### **Expected Output**
```
--- Testing a Rectangle ---
Rectangle Area: 20.0

--- Testing a Square ---
Square Area: 25.0

--- Demonstrating Polymorphism ---
The area of the shape is: 50.0
The area of the shape is: 49.0
```

### **Why This Design Follows LSP**

1.  **No Incorrect Substitution:** The `Square` class no longer pretends to be a `Rectangle`. Therefore, you cannot substitute a `Square` into a method that has specific expectations about how a `Rectangle` behaves (like the `testArea` method in our previous "bad" example). This prevents the bug from ever occurring.

2.  **Honors the Contract:** Both `Rectangle` and `Square` honor the simple contract of the `Shape` interface, which only promises that an area can be calculated via `getArea()`. They both fulfill this promise correctly.

3.  **Clearer Code:** The code is now more explicit and honest. A `Square` has one property (`side`), and a `Rectangle` has two (`width`, `height`). The class structure accurately reflects reality, leading to less confusing code.

4.  **Safe Polymorphism:** The `printShapeArea(Shape shape)` method is a perfect example of safe polymorphism. It only relies on the methods guaranteed by the `Shape` interface. It makes no assumptions about the underlying object's implementation, so it will work correctly with any new `Shape` we create in the future (e.g., `Circle`, `Triangle`), as long as they also implement the `Shape` interface.
### **4. I - Interface Segregation Principle (ISP)**

*   **The Rule:** Clients should not be forced to depend on methods they do not use.
*   **In Simple Terms:** Keep your interfaces small and focused. Don't create "fat" interfaces with lots of methods that not all implementing classes will need.
*   **Why?** Fat interfaces lead to classes having to implement empty or "dummy" methods, which is confusing and brittle.

*   **Analogy: The All-in-One Restaurant Menu**
    *   **Bad (Fat Interface):** A restaurant has a single giant menu called `TheBigMenu` with sections for Breakfast, Lunch, and Dinner. If you are a `Cafe` that only serves breakfast, you are still forced to "implement" the whole menu, leaving the `prepareLunch()` and `prepareDinner()` methods empty.
    *   **Good (Segregated Interfaces):** The restaurant has separate, smaller interfaces: `BreakfastMenu`, `LunchMenu`, `DinnerMenu`. The `Cafe` can just implement the `BreakfastMenu`, which is all it needs.

#### **Example: The `Machine` Interface**

**Bad (Fat Interface):**
```java
// A "fat" interface with too many responsibilities.
interface MultiFunctionMachine {
    void print();
    void scan();
    void fax();
}

class OldPrinter implements MultiFunctionMachine {
    public void print() { /* ... */ }
    public void scan() { throw new UnsupportedOperationException(); /* I can't do this! */ }
    public void fax() { throw new UnsupportedOperationException(); /* Or this! */ }
}
```

**Good (Segregated Interfaces):**
```java
// Small, focused interfaces.
interface Printer { void print(); }
interface Scanner { void scan(); }
interface Fax { void fax(); }

// Now classes only implement what they can actually do.
class OldPrinter implements Printer {
    public void print() { /* ... */ }
}

class ModernPrinter implements Printer, Scanner {
    public void print() { /* ... */ }
    public void scan() { /* ... */ }
}
```

#### **Practice Question (ISP)**

You are designing a system for different types of employees. You start with one big `IEmployee` interface:
`interface IEmployee { void work(); void takeBreak(); void attendMeeting(); }`
You have a `Programmer` who does all three. But then you need to add a `RobotWorker` who can `work()` but cannot `takeBreak()` or `attendMeeting()`. How would you refactor this design to follow ISP?

#### **Solution**
You would segregate the fat `IEmployee` interface into smaller, more specific interfaces.

1.  Create an interface `Workable` with a `work()` method.
2.  Create another interface `Breakable` with a `takeBreak()` method.
3.  Create a third interface `MeetingAttendee` with an `attendMeeting()` method.

Now, the `Programmer` class can implement all three interfaces (`class Programmer implements Workable, Breakable, MeetingAttendee`), while the `RobotWorker` class only needs to implement the `Workable` interface (`class RobotWorker implements Workable`).

---

### **5. D - Dependency Inversion Principle (DIP)**

*   **The Rule:**
    1.  High-level modules should not depend on low-level modules. Both should depend on abstractions.
    2.  Abstractions should not depend on details. Details should depend on abstractions.
*   **In Simple Terms:** Don't let your important, high-level classes depend directly on specific, low-level implementation details. Instead, make both depend on a common **interface** (an abstraction).
*   **Why?** This "decouples" your code. It allows you to easily swap out low-level details (like changing your database from MySQL to PostgreSQL) without having to change your high-level business logic.

*   **Analogy: The Lamp and the Wall Socket**
    *   **Bad (Tight Coupling):** A lamp that is **hard-wired** directly into the wall. The lamp (high-level) depends directly on the wall wiring (low-level). You can't move the lamp, and if it breaks, you need an electrician to fix it.
    *   **Good (Dependency Inversion):** We invent an **abstraction**: the **wall socket interface**. Now, the lamp is built with a standard plug, and the wall wiring terminates in a standard socket. The lamp depends on the socket interface, and the wall wiring depends on the socket interface. They don't depend on each other. You can plug any device into the socket. The dependency has been "inverted."

#### **Example: The `Notification` System**

**Bad (High-level depends on Low-level):**
```java
// Low-level detail
class EmailNotifier {
    public void sendEmail() { /* ... */ }
}

// High-level module
class OrderProcessor {
    private EmailNotifier notifier = new EmailNotifier(); // Direct dependency!

    public void processOrder() {
        // ... process order ...
        notifier.sendEmail(); // Tightly coupled to EmailNotifier
    }
}
// What if we want to send an SMS instead? We have to change the OrderProcessor class!
```

**Good (Both depend on an Abstraction):**
```java
// 1. The Abstraction (the "socket")
interface Notifier {
    void send();
}

// 2. The Low-level details now depend on the abstraction
class EmailNotifier implements Notifier {
    public void send() { /* ... send email ... */ }
}
class SmsNotifier implements Notifier {
    public void send() { /* ... send SMS ... */ }
}

// 3. The High-level module also depends on the abstraction
class OrderProcessor {
    private Notifier notifier;

    // The dependency is "injected" via the constructor
    public OrderProcessor(Notifier notifier) {
        this.notifier = notifier;
    }

    public void processOrder() {
        // ... process order ...
        notifier.send(); // Calls the method on the interface
    }
}

// Now we can easily switch the implementation without changing OrderProcessor
OrderProcessor emailOrder = new OrderProcessor(new EmailNotifier());
OrderProcessor smsOrder = new OrderProcessor(new SmsNotifier());
```

#### **Practice Question (DIP)**

You have a `Car` class (high-level) that creates its engine directly inside its constructor:
`class Car { private Engine engine; public Car() { this.engine = new Engine(); } }`
This is a violation of DIP because `Car` is tightly coupled to the concrete `Engine` class. How would you change this design to follow DIP, allowing you to use different types of engines (e.g., `PetrolEngine`, `ElectricEngine`) in the future?

#### **Solution**
You would "invert the dependency" by using an interface and dependency injection.

1.  Create an `Engine` **interface** with a `start()` method.
2.  Create concrete classes `PetrolEngine` and `ElectricEngine` that `implement` the `Engine` interface.
3.  Change the `Car` class to depend on the `Engine` interface, not the concrete class. The specific engine object will be "injected" (passed in) through the constructor.

**Refactored Code:**
```java
interface Engine { void start(); }
class PetrolEngine implements Engine { /* ... */ }
class ElectricEngine implements Engine { /* ... */ }

class Car {
    private Engine engine; // Depends on the abstraction!

    // The dependency is injected via the constructor
    public Car(Engine engine) {
        this.engine = engine;
    }

    public void startCar() {
        engine.start();
    }
}

// Now we can create cars with different engines easily:
Car petrolCar = new Car(new PetrolEngine());
Car electricCar = new Car(new ElectricEngine());
```



## **Quick Revision Guide: JDBC Fundamentals**


### **1. JDBC Overview**

*   **Definition:** JDBC (Java Database Connectivity) is a standard **Java API** used to perform database operations from a Java application. It provides a set of classes and interfaces that allow for a uniform way to connect to and interact with various relational databases (like MySQL, Oracle, PostgreSQL).
*   **Analogy:** JDBC is a **universal adapter**. The Java application has a standard plug (the JDBC API). Each database provider (MySQL, Oracle) creates a special socket for that plug (the **JDBC Driver**). As long as you have the right adapter (driver), your standard plug (Java code) can connect to any socket (database).

---

### **2. JDBC Driver Types**

There are four types of JDBC drivers, though Types 2 and 4 are the most relevant today.

*   **Type 1: JDBC-ODBC Bridge Driver:** Translates JDBC calls into ODBC (Open Database Connectivity) calls. (Largely obsolete).
*   **Type 2: Native-API Driver:** A mix of Java code and native code (C/C++). It translates JDBC calls into calls on the client-side API of the database. Requires native libraries to be installed on the client machine.
*   **Type 3: Network-Protocol Driver:** A pure Java driver that communicates with a middleware server, which then translates the requests into the database-specific protocol.
*   **Type 4: Thin Driver (Database-Protocol Driver):** A **pure Java** driver that communicates directly with the database server using its native protocol. This is the **most common and recommended type** because it is platform-independent and does not require any special software on the client side. The MySQL Connector/J is a Type 4 driver.

---

### **3. The 6 Steps to Perform a JDBC Operation**

This is a very common exam question.

1.  **Load and Register the Driver:** (Often automatic in modern JDBC 4.0+) Tell the `DriverManager` which driver to use.
    *   `Class.forName("com.mysql.cj.jdbc.Driver");`
2.  **Establish a Connection:** Create a `Connection` object using the database URL, username, and password.
    *   `Connection con = DriverManager.getConnection(url, user, pass);`
3.  **Create a Statement:** Create a `Statement` or `PreparedStatement` object to execute SQL queries.
    *   `PreparedStatement pstmt = con.prepareStatement(sql);`
4.  **Execute the Query:** Run the SQL query. The method you call depends on the type of query.
    *   `ResultSet rs = pstmt.executeQuery();` (for `SELECT`)
    *   `int rowsAffected = pstmt.executeUpdate();` (for `INSERT`, `UPDATE`, `DELETE`)
5.  **Process the Results:** If you executed a `SELECT` query, iterate through the `ResultSet` object to retrieve the data.
    *   `while (rs.next()) { ... }`
6.  **Close the Resources:** **Crucially**, close the `ResultSet`, `Statement`, and `Connection` objects to release database and memory resources. This is best done with a `try-with-resources` statement or in a `finally` block.

---

### **4. Common JDBC Components**

*   **`DriverManager`:** A factory class that manages a set of JDBC drivers. Its primary role is to provide a `Connection` to the database via its `getConnection()` method.

*   **`Connection`:** An interface representing a single session with the database. It's the context within which all SQL statements are executed and results are returned.

*   **`Statement` vs. `PreparedStatement`:**
    *   **`Statement`:** Used for executing simple, static SQL queries. It is vulnerable to **SQL Injection** attacks.
        ```java
        Statement stmt = con.createStatement();
        ResultSet rs = stmt.executeQuery("SELECT * FROM users WHERE id = " + userId); // UNSAFE!
        ```
    *   **`PreparedStatement`:** Used for executing pre-compiled SQL queries with parameters (`?`). It is **safer** (prevents SQL injection) and often performs better. **This is the preferred choice.**
        ```java
        PreparedStatement pstmt = con.prepareStatement("SELECT * FROM users WHERE id = ?");
        pstmt.setInt(1, userId); // Safely sets the parameter
        ResultSet rs = pstmt.executeQuery();
        ```

*   **`ResultSet`:** An interface representing the data returned from a `SELECT` query. It's like a cursor pointing to one row of data at a time. You use its `next()` method to move to the next row.

---

### **5. Connection Establishment**

*   **Definition:** This is the process of creating a `Connection` object. It requires a **JDBC URL**, which is a specially formatted string that tells the `DriverManager` which driver to use and which database to connect to.
*   **JDBC URL Format:** It always follows the pattern `jdbc:<subprotocol>:<subname>`.
    *   **MySQL Example:** `jdbc:mysql://localhost:3306/mydatabase`
        *   `jdbc`: The standard protocol.
        *   `mysql`: The subprotocol for the MySQL driver.
        *   `//localhost:3306/mydatabase`: The subname, containing the host, port, and database name.
*   **Code Example:**
    ```java
    String url = "jdbc:mysql://localhost:3306/login_app_db";
    String user = "root";
    String password = "password";
    try {
        Connection connection = DriverManager.getConnection(url, user, password);
        System.out.println("Connection established successfully!");
        connection.close();
    } catch (SQLException e) {
        System.err.println("Connection failed: " + e.getMessage());
    }
    ```

---

### **6. SQL Fundamentals & CRUD Operations with JDBC**

**CRUD** stands for **C**reate, **R**ead, **U**pdate, **D**elete. These are the four basic functions of persistent storage.

#### **a) READ (Executing `SELECT` Queries and Working with `ResultSet`)**

This operation retrieves data from the database.

*   **`executeQuery()`:** This method is used for `SELECT` statements and returns a `ResultSet` object.
*   **Working with `ResultSet`:**
    *   `rs.next()`: Moves the cursor to the next row. It returns `false` when there are no more rows. This is typically used as the condition in a `while` loop.
    *   `rs.getString("column_name")`, `rs.getInt("column_name")`: These "getter" methods retrieve the value from a specific column in the current row.

*   **Code Example:**
    ```java
    // Assume 'con' is a valid Connection object
    String sql = "SELECT id, username FROM users WHERE username = ?";
    try (PreparedStatement pstmt = con.prepareStatement(sql)) {
        pstmt.setString(1, "btech");
        try (ResultSet rs = pstmt.executeQuery()) {
            // Check if any result was found
            if (rs.next()) {
                int id = rs.getInt("id");
                String username = rs.getString("username");
                System.out.println("User found: ID=" + id + ", Username=" + username);
            } else {
                System.out.println("User not found.");
            }
        }
    }
    ```

#### **b) CREATE, UPDATE, DELETE (Using `executeUpdate()`)**

These operations modify data in the database.

*   **`executeUpdate()`:** This method is used for `INSERT`, `UPDATE`, and `DELETE` statements. It does **not** return a `ResultSet`. Instead, it returns an `int` representing the **number of rows affected** by the query.

**Code Example: CREATE (`INSERT`)**
```java
String sql = "INSERT INTO users (username, password) VALUES (?, ?)";
try (PreparedStatement pstmt = con.prepareStatement(sql)) {
    pstmt.setString(1, "student");
    pstmt.setString(2, "1234");
    
    int rowsAffected = pstmt.executeUpdate();
    System.out.println(rowsAffected + " row(s) inserted."); // Should print "1 row(s) inserted."
}
```

**Code Example: UPDATE**
```java
String sql = "UPDATE users SET password = ? WHERE username = ?";
try (PreparedStatement pstmt = con.prepareStatement(sql)) {
    pstmt.setString(1, "new_password_5678");
    pstmt.setString(2, "student");
    
    int rowsAffected = pstmt.executeUpdate();
    System.out.println(rowsAffected + " row(s) updated.");
}
```

**Code Example: DELETE**
```java
String sql = "DELETE FROM users WHERE username = ?";
try (PreparedStatement pstmt = con.prepareStatement(sql)) {
    pstmt.setString(1, "student");
    
    int rowsAffected = pstmt.executeUpdate();
    System.out.println(rowsAffected + " row(s) deleted.");
}
```
