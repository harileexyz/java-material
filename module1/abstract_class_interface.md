
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

### **5. Practice Questions & Solutions**
*(The practice questions and solutions from the previous response would follow here, as they are relevant and test these concepts effectively.)*