
---
---

## **Live Class Revision Guide: Inheritance & Runtime Polymorphism**

**Objective:** A rapid, high-impact review of how classes are related through inheritance and how this enables the powerful feature of runtime polymorphism.

---

### **Topic 1: Inheritance Fundamentals (Superclass & Subclass)**

#### **Quick Revision Notes:**

*   **Inheritance:** The process where one class (**subclass**) acquires the properties and behaviors of another class (**superclass**).
*   **Purpose:** The primary goal is **code reusability**.
*   **Relationship:** It establishes an **"is-a"** relationship. A `Car` *is a* `Vehicle`.
*   **`extends` Keyword:** This is the keyword used in Java to create an inheritance link. `class Car extends Vehicle {}`.
*   **Superclass (Parent/Base):** The general class that is being inherited from (e.g., `Vehicle`).
*   **Subclass (Child/Derived):** The specialized class that inherits. It gets all `public` and `protected` members for free and can add its own. (e.g., `Car`).

*   **Analogy to Remember:** **The Smartphone Family**
    *   **Superclass:** A generic `Phone`. All phones can `makeCall()` and have a `phoneNumber`.
    *   **Subclass:** A `Smartphone`. It **is a** `Phone`, so it inherits the ability to `makeCall()`. But it also adds its own unique features, like `browseInternet()` and `takePhoto()`.

---

### **Topic 2: Types of Inheritance in Java**

It's important to understand the different ways classes can be structured in a hierarchy and which of these structures Java supports directly with classes.

#### **a) Single Inheritance (Supported)**
This is the simplest and most common form. A single subclass extends a single superclass.

*   **Diagram:** `Superclass A` ← `Subclass B`
*   **Analogy:** A `Car` inherits from a `Vehicle`. One parent, one child.

```java
class Vehicle { /* ... */ }
class Car extends Vehicle { /* ... */ }
```

#### **b) Multilevel Inheritance (Supported)**
A subclass acts as a superclass for another class, creating a chain of inheritance.

*   **Diagram:** `Grandparent A` ← `Parent B` ← `Child C`
*   **Analogy:** `Animal` ← `Dog` ← `Puppy`. A `Puppy` inherits all the features of a `Dog`, which in turn inherits all the features of an `Animal`.
*   **Example:**
    ```java
    class Animal {
        void eat() { System.out.println("Eating..."); }
    }
    class Dog extends Animal { // Inherits eat()
        void bark() { System.out.println("Barking..."); }
    }
    class Puppy extends Dog { // Inherits eat() and bark()
        void weep() { System.out.println("Weeping..."); }
    }
    // A Puppy object can eat(), bark(), and weep().
    ```

#### **c) Hierarchical Inheritance (Supported)**
Multiple, independent subclasses extend the *same* single superclass.

*   **Diagram:** `Subclass B` → `Superclass A` ← `Subclass C`
*   **Analogy:** `Vehicle` is the parent. `Car` extends `Vehicle`, and `Motorcycle` also extends `Vehicle`. `Car` and `Motorcycle` are siblings.
*   **Example:**
    ```java
    class Vehicle { /* ... */ }
    class Car extends Vehicle { /* ... */ }
    class Motorcycle extends Vehicle { /* ... */ }
    ```

#### **d) Multiple & Hybrid Inheritance (NOT Supported via Classes)**
*   **Multiple Inheritance:** A single class tries to extend **two or more** parent classes. `A` → `C` ← `B`
*   **Hybrid Inheritance:** A mix of different types, such as Hierarchical and Multiple.
*   **Why Not? The Diamond Problem:** Java avoids this to prevent ambiguity. If `Class C` extends `A` and `B`, and both `A` and `B` have a method called `doWork()`, which version should `C` inherit? This is the "Diamond Problem."
*   **Java's Solution:** A class can **implement multiple interfaces**. This allows a class to promise multiple sets of behaviors without the ambiguity of inheriting implemented code.

---
### **Topic 3: `protected` Members & The `super` Keyword**

#### **1. `protected` Members**
*   **Quick Description:** A special access modifier designed for inheritance.
*   **Visibility:** Visible within its own class, the **same package**, and to any **subclass** (even in a different package).
*   **Analogy to Remember:** A **Family Recipe Book**. Only family members can access it.

#### **2. The `super` Keyword**
*   **Quick Description:** A reference to the immediate **superclass object**.
*   **Two Main Uses:**
    1.  **`super()`:** Calls the parent constructor. Must be the first line.
    2.  **`super.method()`:** Calls the parent's version of a method.
*   **Analogy to Remember:** **Talking to Your Parent**.

---
### **Topic 4: The Constructor Calling Order**

#### **Quick Revision Notes:**

*   **The Golden Rule:** The **superclass constructor is always executed first**.
*   **The Chain:** This forms a "constructor chain" from the topmost superclass down to the subclass being created.
*   **How it Works:** The compiler implicitly inserts `super()` as the first line of any constructor.

#### **Live Practice Question 1: Constructor Chaining**
**(This question and solution remain the same as the previous version, as it's a perfect fit here.)**

**Question:** What will be the output when we create a `Manager` object?

```java
class Employee {
    String employeeType = "Generic";
    public Employee() { System.out.println("1. Employee constructor called."); }
    public Employee(String type) {
        this.employeeType = type;
        System.out.println("2. Employee parameterized constructor called.");
    }
}
class Manager extends Employee {
    public Manager() {
        super("Salaried"); 
        System.out.println("3. Manager constructor called.");
    }
}
public class Main {
    public static void main(String[] args) {
        System.out.println("Creating a Manager...");
        Manager mgr = new Manager();
        System.out.println("Manager Type: " + mgr.employeeType);
    }
}
```

#### **Live Solution & Explanation**

**Predicted Output:**
```
Creating a Manager...
2. Employee parameterized constructor called.
3. Manager constructor called.
Manager Type: Salaried
```
**Explanation:** The `Manager` constructor explicitly calls the parent's parameterized constructor with `super("Salaried")`, so the no-argument parent constructor is skipped. The parent constructor always runs before the child's constructor body.

---

### **Topic 5: Method Overriding & Dynamic Method Dispatch**

#### **1. Method Overriding**
*   **Quick Description:** A subclass provides its own specific implementation for a method that is already defined in its superclass. The method signature must be identical.
*   **`@Override` Annotation:** A best-practice marker to tell the compiler you intend to override a method, helping you catch typos.

#### **2. Dynamic Method Dispatch**
*   **Quick Description:** The process where the call to an **overridden method is resolved at runtime**. The JVM looks at the **actual object** to decide which version of the method to run.
*   **Analogy to Remember:** **The Universal Remote Control**. The `start()` button is the same, but the action dispatched is different depending on whether the remote is pointing at a `Car` or a `Motorcycle`.

#### **Live Practice Question 2: The `Sound` System (Hierarchical Inheritance)**
Let's demonstrate Dynamic Method Dispatch using a hierarchical inheritance structure.

**Question:**
1.  Create a base class `Animal` with a `makeSound()` method that prints "The animal makes a generic sound."
2.  Create two subclasses, `Dog` and `Cat`, that **both extend `Animal`**.
3.  **Override** the `makeSound()` method in both subclasses to print "Woof!" and "Meow!", respectively.
4.  Create a `static` method `triggerSound(Animal animal)`. This method will take any `Animal` object and call its `makeSound()` method.
5.  In `main`, create a `Dog` and a `Cat` object and pass both to the *same* `triggerSound()` method to observe the different outputs.

#### **Live Solution & Explanation**
```java
class Animal {
    public void makeSound() {
        System.out.println("The animal makes a generic sound.");
    }
}

class Dog extends Animal { // Child 1
    @Override
    public void makeSound() {
        System.out.println("Woof!");
    }
}

class Cat extends Animal { // Child 2
    @Override
    public void makeSound() {
        System.out.println("Meow!");
    }
}

public class Main {
    // This method is polymorphic.
    public static void triggerSound(Animal animal) {
        System.out.print("Triggering sound... It says: ");
        // Dynamic Method Dispatch: JVM calls the correct method based on the actual object.
        animal.makeSound();
    }

    public static void main(String[] args) {
        // We use the parent 'Animal' as the reference type.
        Animal myDog = new Dog();
        Animal myCat = new Cat();
        
        // Pass different sibling objects to the SAME method.
        triggerSound(myDog); // Will call Dog's makeSound()
        triggerSound(myCat); // Will call Cat's makeSound()
    }
}
```
**Explanation:** "This demonstrates hierarchical inheritance where both `Dog` and `Cat` inherit from `Animal`. The `triggerSound` method works flawlessly with both because it's programmed to the general `Animal` abstraction. This is the power of combining inheritance with polymorphism."