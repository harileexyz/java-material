
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

## **✍️ Inheritance Worksheet**

**Name:** ___________________________
**Roll No:** ___________________________

### **Part A: Theory Questions**

1.  What is the main purpose of inheritance in OOP?
    ________________________________________________________________
2.  Explain the difference between a superclass and a subclass.
    ________________________________________________________________
3.  What is the "is-a" test and why is it useful? Give one example where it applies and one where it does not.
    ________________________________________________________________
4.  Why does Java not support multiple inheritance with classes? What problem does it avoid?
    ________________________________________________________________
5.  What are the two primary uses of the `super` keyword in a subclass?
    ________________________________________________________________

---

### **Part B: Code Writing and Analysis**

**❓ Q1. Create a Hierarchy**
Design a simple three-level hierarchy (multilevel inheritance).
1.  Create a base class `Device` with a `String brand` and a method `turnOn()`.
2.  Create a subclass `Phone` that extends `Device`. Add a method `makeCall()`.
3.  Create a subclass `Smartphone` that extends `Phone`. Add a method `browseInternet()`.
4.  In a `main` method, create a `Smartphone` object and call all three methods (`turnOn()`, `makeCall()`, and `browseInternet()`) to show that it has inherited all behaviors.

**❓ Q2. Analyze the Code**
What will be the output of the following code? Explain why, step by step, focusing on the constructors and the `super` keyword.

```java
class A {
    public A() {
        System.out.println("Constructor of class A");
    }
}

class B extends A {
    public B() {
        // super(); // Implicit call to parent constructor is here
        System.out.println("Constructor of class B");
    }
}

class C extends B {
    public C() {
        System.out.println("Constructor of class C");
    }
}

public class Main {
    public static void main(String[] args) {
        C c_object = new C();
    }
}


---

## **✅ Solutions to Worksheet**

### **Part A: Theory Questions - Solutions**

1.  **What is the main purpose of inheritance in OOP?**
    The main purpose is **code reusability**. It allows a new class to reuse fields and methods from an existing class, avoiding code duplication and establishing a logical hierarchy.

2.  **Explain the difference between a superclass and a subclass.**
    A **superclass** (or parent class) is the class whose features are being inherited. It is a more general class. A **subclass** (or child class) is the class that does the inheriting. It is a more specialized class that gets the features of the superclass and can add its own.

3.  **What is the "is-a" test and why is it useful? Give one example where it applies and one where it does not.**
    The "is-a" test is a simple check to see if an inheritance relationship is logical. If you can say "Subclass *is a* Superclass," it's a good fit.
    *   **Applies:** A `Triangle` **is a** `Shape`. (Logical inheritance).
    *   **Does not apply:** A `Wheel` **is a** `Car`. (Incorrect. A wheel is *part of* a car. This represents composition, not inheritance).

4.  **Why does Java not support multiple inheritance with classes? What problem does it avoid?**
    Java does not support multiple inheritance with classes to avoid the **Diamond Problem**. This problem occurs when a class `D` inherits from two classes `B` and `C`, both of which inherit from a single class `A` that has a method `m()`. If both `B` and `C` override `m()`, the compiler doesn't know which version of `m()` class `D` should inherit, creating ambiguity.

5.  **What are the two primary uses of the `super` keyword in a subclass?**
    1.  To call a **superclass's constructor** (`super(...)`). This must be the first line in the subclass constructor.
    2.  To call a **superclass's method or access its field** (`super.method()` or `super.field`), especially when the method is overridden or the field is hidden by the subclass.

### **Part B: Code Writing and Analysis - Solutions**

**❓ Q1. Create a Hierarchy - Solution**
```java
// Level 1: Base Class
class Device {
    String brand = "Generic Brand";
    public void turnOn() {
        System.out.println("Device is turning on.");
    }
}

// Level 2: Subclass
class Phone extends Device {
    public void makeCall() {
        System.out.println("Making a call...");
    }
}

// Level 3: Sub-subclass
class Smartphone extends Phone {
    public void browseInternet() {
        System.out.println("Browsing the internet...");
    }
}

// Main class for testing
public class Main {
    public static void main(String[] args) {
        Smartphone myPhone = new Smartphone();
        myPhone.brand = "Samsung"; // Inherited from Device

        System.out.println("My phone is a " + myPhone.brand);
        myPhone.turnOn();         // Inherited from Device
        myPhone.makeCall();       // Inherited from Phone
        myPhone.browseInternet(); // Its own method
    }
}
```

**❓ Q2. Analyze the Code - Solution**

**Predicted Output:**
```
Constructor of class A
Constructor of class B
Constructor of class C
```
**Explanation:**
1.  When `new C()` is called in `main`, the constructor for class `C` is invoked.
2.  The very first thing a constructor does (implicitly, if not written) is call its parent's constructor using `super()`. So, the `C` constructor immediately calls the `B` constructor.
3.  Similarly, the first thing the `B` constructor does is implicitly call its parent's constructor, `super()`. So, the `B` constructor immediately calls the `A` constructor.
4.  The `A` constructor runs first and prints "Constructor of class A".
5.  Control then returns to the `B` constructor, which finishes its execution and prints "Constructor of class B".
6.  Finally, control returns to the `C` constructor, which finishes its execution and prints "Constructor of class C".
This shows that constructors are executed in a chain from the top of the hierarchy down to the bottom.