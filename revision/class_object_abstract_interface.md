
---
---

## **End-to-End Study Guide: The Blueprints of OOP - Classes, Abstract Classes, and Interfaces**

This module introduces the core structural elements of Object-Oriented Programming in Java. We will start with the most fundamental unit—the **class**—and then explore its specialized forms, abstract classes and interfaces. Mastering these concepts is essential to understanding how OOP works.

### **Table of Contents**
1.  **Classes and Objects:** The Foundation of OOP
2.  **Constructors:** The Object Initializers
3.  **Abstract Classes:** The Incomplete Blueprint
4.  **Interfaces:** The Pure Contract

---

### **1. Classes and Objects: The Foundation of OOP**

#### **1.1. Detailed Description**

In the real world, we understand things as objects. A car is an object, a student is an object, and a bank account is an object. Each of these has two key characteristics:
1.  **State (Attributes):** The properties or data that describe an object. A `Student` object has a *name*, a *roll number*, and a *major*.
2.  **Behavior (Methods):** The actions an object can perform. A `Student` object can *enroll in a course*, *study*, and *take an exam*.

In Java, a **class** is a **blueprint** or template that defines this common structure. It's a user-defined data type that specifies what fields (state) and methods (behavior) its objects will have. A class is a logical construct; it doesn't exist in memory until you create an object from it.

An **object** (also called an **instance**) is a concrete, physical entity created from a class blueprint. When an object is created, it gets its own block of memory and its own set of instance variables to store its unique state.

**Analogy to Remember: The Cookie Cutter**
*   **Class:** The **cookie cutter**. It defines the shape (e.g., a star) and properties for all cookies made with it. The cutter itself is not a cookie.
*   **Object:** An **actual cookie**. Each cookie you cut is a separate object. They were all made from the same cutter (class), so they have the same shape, but each can have its own unique state (one might have sprinkles, another might be slightly burnt).

#### **1.2. Example: The `Student` Class**

Let's create a blueprint for a student.

```java
// File: Student.java
// This is the blueprint for all Student objects.
public class Student {
    // --- 1. Fields (Instance Variables) ---
    // These define the STATE of a Student. Each student object will have its own copy.
    String name;
    int rollNumber;
    String major;

    // --- 2. Methods ---
    // These define the BEHAVIOR of a Student.
    // Notice how methods can use the object's fields.
    public void introduce() {
        // 'this' keyword refers to the current object.
        System.out.println("Hello, my name is " + this.name + " and my roll number is " + this.rollNumber + ".");
    }

    public void changeMajor(String newMajor) {
        this.major = newMajor;
        System.out.println(this.name + " has changed their major to " + this.major + ".");
    }
}
```

#### **1.3. Live Practice Question: The `Dog` Class**

**Question:** Create a simple `Dog` class.
1.  It should have three **fields**: `name` (String), `breed` (String), and `age` (int).
2.  It should have two **methods**: `bark()` which prints "Woof! Woof!", and `displayInfo()` which prints all the dog's details (name, breed, and age).
3.  In a `main` method, create two different `Dog` objects, set their details, and call their methods to show they are separate instances.

#### **Solution**
```java
// The Dog class blueprint
class Dog {
    // Fields
    String name;
    String breed;
    int age;

    // Methods
    public void bark() {
        System.out.println("Woof! Woof!");
    }

    public void displayInfo() {
        System.out.println("Name: " + name + ", Breed: " + breed + ", Age: " + age);
    }
}

// Main class to test our blueprint
public class Main {
    public static void main(String[] args) {
        // Create the first Dog object
        Dog dog1 = new Dog();
        dog1.name = "Buddy";
        dog1.breed = "Golden Retriever";
        dog1.age = 3;

        // Create a second, separate Dog object
        Dog dog2 = new Dog();
        dog2.name = "Lucy";
        dog2.breed = "Poodle";
        dog2.age = 5;

        System.out.println("Details of the first dog:");
        dog1.displayInfo();
        dog1.bark();

        System.out.println("\nDetails of the second dog:");
        dog2.displayInfo();
        dog2.bark();
    }
}
```

---

### **2. Constructors: The Object Initializers**

#### **2.1. Detailed Description**

In the previous example, we created an object and then set its fields line by line. This is risky—what if we forget to set a field? The object would be in an incomplete or invalid state.

A **constructor** solves this problem. It is a special block of code, similar to a method, that is **called automatically when you create an object** of a class (using the `new` keyword). Its primary purpose is to **initialize the instance variables**, ensuring the object starts its life in a valid and consistent state.

**Rules for Creating a Constructor:**
1.  A constructor's name must be **exactly the same** as the class name.
2.  A constructor **cannot have a return type**, not even `void`.
3.  If you don't provide any constructor, Java supplies a "default constructor" that takes no arguments and does nothing.

**Analogy to Remember: The New Car Assembly Line**
*   **`new Car()`:** You place an order for a new car.
*   **Constructor:** The **factory assembly line process** is triggered. It ensures the car is built with all its essential parts (engine, wheels, seats) before it is delivered to you. You can't get an empty shell of a car; the constructor guarantees a complete, usable object.

#### **2.2. Example: The `Book` Class with a Constructor**

Let's create a `Book` class that requires a title and author upon creation.

```java
// File: Book.java
public class Book {
    // Fields are often made private to enforce encapsulation
    private String title;
    private String author;

    // --- Parameterized Constructor ---
    // This constructor takes parameters to initialize the object's fields.
    public Book(String bookTitle, String bookAuthor) {
        System.out.println("Book constructor called...");
        // 'this' keyword is used to distinguish the instance variable from the parameter
        this.title = bookTitle;
        this.author = bookAuthor;
    }

    public void displayDetails() {
        System.out.println("Title: '" + this.title + "', Author: " + this.author);
    }
}

// File: Library.java (Main class)
public class Library {
    public static void main(String[] args) {
        // To create a Book object, we MUST now provide a title and author.
        // The constructor is called automatically.
        Book book1 = new Book("The Hobbit", "J.R.R. Tolkien");
        Book book2 = new Book("1984", "George Orwell");

        // The objects are guaranteed to be in a valid state.
        book1.displayDetails();
        book2.displayDetails();
    }
}
```

#### **2.3. Live Practice Question: The `Laptop` Constructor**

**Question:** Create a `Laptop` class.
1.  Have `private` fields for `brand` (String) and `ramSizeGB` (int).
2.  Create a **constructor** that accepts the brand and RAM size as arguments and initializes the fields.
3.  Add a `public` method `displaySpecs()` that prints the laptop's specifications.
4.  In a `main` method, create a `Laptop` object using the constructor and call its `displaySpecs()` method.

#### **Solution**
```java
class Laptop {
    private String brand;
    private int ramSizeGB;

    // Constructor to initialize the Laptop object
    public Laptop(String brand, int ramSizeGB) {
        this.brand = brand;
        this.ramSizeGB = ramSizeGB;
    }

    public void displaySpecs() {
        System.out.println("Laptop Specs -> Brand: " + this.brand + ", RAM: " + this.ramSizeGB + "GB");
    }
}

public class Main {
    public static void main(String[] args) {
        // Create an object using the constructor
        Laptop myLaptop = new Laptop("Dell", 16);
        myLaptop.displaySpecs();
        
        Laptop gamingLaptop = new Laptop("Asus ROG", 32);
        gamingLaptop.displaySpecs();
    }
}
```

---

### **3. Abstract Classes: The Incomplete Blueprint**

#### **3.1. Detailed Description**

Now that we understand a class is a complete blueprint, imagine a blueprint that is **intentionally left incomplete**. This is an **abstract class**. It's a special type of class that cannot be used to create objects directly (`new AbstractClass()` is illegal). Its purpose is to serve as a common **base template** for a family of related subclasses.

An abstract class is a blend of specification and implementation:
*   It can have **concrete methods** (regular methods with a full body) to provide shared functionality to all its children.
*   It can have **abstract methods** (methods with no body, just a signature) to **force** its children to provide their own unique implementation for that behavior.

It enforces an **"is-a"** relationship. A `Dog` *is an* `Animal`.

**Analogy to Remember: A "Vehicle" Blueprint**
*   You can't go to a factory and ask them to build you "a vehicle." That's too general. "Vehicle" is an **abstract concept**.
*   The blueprint for a `Vehicle` (the abstract class) can define **common, concrete behaviors** like `honkHorn()` (all vehicles have a horn) and **common attributes** like `speed`.
*   But it must also define an **abstract behavior** like `startEngine()`, because *how* an engine starts is completely different for a `Car`, an `ElectricScooter`, and a `Motorcycle`. The abstract class forces each specific type of vehicle to define its own `startEngine()` method.

#### **3.2. Example: The `Shape` Abstract Class**

All shapes can be drawn, but the way you draw a circle is different from a square.

```java
// This blueprint is incomplete. You cannot create a generic "Shape" object.
abstract class Shape {
    String color;

    public Shape(String color) {
        this.color = color;
    }

    // --- Concrete Method ---
    // All subclasses will inherit this exact method.
    public void displayColor() {
        System.out.println("The color of the shape is " + this.color);
    }

    // --- Abstract Method ---
    // Has no body. It's a rule that any non-abstract child MUST implement this method.
    public abstract void draw();
}

// Concrete subclass 1
class Circle extends Shape {
    public Circle(String color) { super(color); }

    // Providing the mandatory implementation for the abstract method.
    @Override
    public void draw() {
        System.out.println("Drawing a circle: O");
    }
}

// Concrete subclass 2
class Square extends Shape {
    public Square(String color) { super(color); }

    @Override
    public void draw() {
        System.out.println("Drawing a square: []");
    }
}

public class Main {
    public static void main(String[] args) {
        // Shape myShape = new Shape("Red"); // COMPILE ERROR! Cannot instantiate an abstract class.

        Shape circle = new Circle("Blue");
        circle.displayColor(); // Calling inherited concrete method
        circle.draw();         // Calling child's implemented method

        Shape square = new Square("Red");
        square.displayColor();
        square.draw();
    }
}
```

#### **3.3. Live Practice Question: The `Animal` Abstract Class**

**Question:** Create an `Animal` abstract class.
1.  It should have a **concrete method** `sleep()` that prints "This animal is sleeping."
2.  It should have an **abstract method** `makeSound()`.
3.  Create two concrete subclasses, `Lion` and `Duck`, that `extend Animal`.
4.  Implement the `makeSound()` method in each subclass to print "Roar!" and "Quack!", respectively.
5.  In `main`, create a `Lion` and a `Duck` object. Call both the `sleep()` and `makeSound()` methods on each to demonstrate they have both shared and unique behaviors.

#### **Solution**
```java
abstract class Animal {
    // Concrete method - shared by all children
    public void sleep() {
        System.out.println("This animal is sleeping.");
    }

    // Abstract method - must be implemented by children
    public abstract void makeSound();
}

class Lion extends Animal {
    @Override
    public void makeSound() {
        System.out.println("The lion says: Roar!");
    }
}

class Duck extends Animal {
    @Override
    public void makeSound() {
        System.out.println("The duck says: Quack!");
    }
}

public class Main {
    public static void main(String[] args) {
        Lion simba = new Lion();
        System.out.println("--- Lion's Actions ---");
        simba.makeSound(); // Its own implementation
        simba.sleep();     // Inherited implementation

        Duck donald = new Duck();
        System.out.println("\n--- Duck's Actions ---");
        donald.makeSound();
        donald.sleep();
    }
}
```

---

### **4. Interfaces: The Pure Contract**

#### **4.1. Detailed Description**

If an abstract class is an *incomplete blueprint*, an interface is a **pure contract** or a **list of rules**. It has no implementation details at all. It simply defines a set of method signatures that a class **must** implement if it claims to adhere to that interface.

An interface defines a **"can-do"** relationship. It doesn't care *what* an object is, only *what it is capable of doing*.

*   A `Bird` can fly.
*   An `Airplane` can fly.
*   A `Superhero` can fly.

These three classes are completely unrelated, but they all share the `Flyable` capability. An interface allows us to treat them all as "things that can fly."

**Key Features:**
*   Methods in an interface are `public` and `abstract` by default.
*   You use the `implements` keyword for a class to use an interface.
*   A class can `extends` only **one** superclass, but it can `implements` **multiple** interfaces.

**Analogy to Remember: A USB Port**
*   The **USB specification** is the **interface**. It defines the rules: a port must have a specific shape and must be able to transfer data and provide power. It doesn't say *what kind of device* it is.
*   A **pendrive**, a **keyboard**, and a **smartphone** are all different classes that **implement** the USB interface. They are all completely different devices, but you can plug any of them into the same USB port (a method that accepts the `USB` interface type) and it will work.

#### **4.2. Example: The `Drivable` Interface**
```java
// The contract: Anything that is Drivable MUST be able to start, stop, and turn.
interface Drivable {
    void start();
    void stop();
    void turn(String direction);
}

// A Car is a thing that implements the Drivable contract.
class Car implements Drivable {
    @Override
    public void start() {
        System.out.println("Car engine started.");
    }
    @Override
    public void stop() {
        System.out.println("Car is braking.");
    }
    @Override
    public void turn(String direction) {
        System.out.println("Car is turning " + direction + ".");
    }
}

// A Lawnmower is a completely different thing, but it also implements the Drivable contract.
class Lawnmower implements Drivable {
    @Override
    public void start() {
        System.out.println("Lawnmower engine started with a pull-cord.");
    }
    @Override
    public void stop() {
        System.out.println("Lawnmower blade disengaged.");
    }
    @Override
    public void turn(String direction) {
        System.out.println("Lawnmower is being pushed to the " + direction + ".");
    }
}

public class Main {
    // This method can accept ANY object, as long as it implements the Drivable interface.
    public static void testDrive(Drivable vehicle) {
        System.out.println("\n--- Testing a new vehicle ---");
        vehicle.start();
        vehicle.turn("left");
        vehicle.stop();
    }

    public static void main(String[] args) {
        Drivable myCar = new Car();
        Drivable myMower = new Lawnmower();

        testDrive(myCar);
        testDrive(myMower);
    }
}
```

#### **4.3. Live Practice Question: The `Playable` Interface**

**Question:** Imagine a media player application. You need a way to handle different types of media.
1.  Create an interface named `Playable` with a single abstract method: `play()`.
2.  Create two classes, `Song` and `Video`, that both `implement` the `Playable` interface.
3.  The `Song` class's `play()` method should print "Playing song: [title]". It should have a `title` field initialized via a constructor.
4.  The `Video` class's `play()` method should print "Showing video: [filename]". It should have a `filename` field initialized via a constructor.
5.  In `main`, create a `Song` object and a `Video` object. Create a `Playable[]` array to hold both of them. Loop through the array and call the `play()` method on each element to demonstrate polymorphism.

#### **Solution**
```java
// The interface contract
interface Playable {
    void play();
}

// First class that fulfills the contract
class Song implements Playable {
    private String title;
    public Song(String title) { this.title = title; }

    @Override
    public void play() {
        System.out.println("Playing song: " + this.title);
    }
}

// A different class that also fulfills the contract
class Video implements Playable {
    private String filename;
    public Video(String filename) { this.filename = filename; }

    @Override
    public void play() {
        System.out.println("Showing video: " + this.filename);
    }
}

public class Main {
    public static void main(String[] args) {
        // Create an array of the INTERFACE type to hold different object types
        Playable[] mediaPlaylist = new Playable[2];

        mediaPlaylist[0] = new Song("Bohemian Rhapsody by Queen");
        mediaPlaylist[1] = new Video("My_Vacation.mp4");

        System.out.println("--- Starting Playlist ---");
        // Loop through the playlist and call play() on each item.
        // Java's polymorphism ensures the correct method is called for each object.
        for (Playable media : mediaPlaylist) {
            media.play();
        }
    }
}
```