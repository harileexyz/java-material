
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
### **Topic 2: `protected` Members & The `super` Keyword**

#### **1. `protected` Members**
*   **Quick Description:** A `protected` member is a special access modifier designed for inheritance.
*   **Visibility:** It is visible within its own class, within other classes in the **same package**, and to any **subclass**, even if the subclass is in a different package.
*   **Analogy to Remember:** A **Family Recipe Book**. Only family members can access it. Immediate family (same package) and children who have moved out (subclasses in different packages) can still use the recipes. A stranger (unrelated class) cannot.

#### **2. The `super` Keyword**
*   **Quick Description:** `super` is a keyword that acts as a reference to the immediate **superclass object**.
*   **Two Main Uses:**
    1.  **`super()` (Calling Parent Constructor):** Used to call a constructor from the parent class. It **must be the first line** in the subclass's constructor.
    2.  **`super.method()` or `super.field`:** Used to access a method or field from the parent class, especially when the subclass has overridden that method or hidden that field.

*   **Analogy to Remember:** **Talking to Your Parent**.
    *   `super()`: When you are born (child constructor runs), your existence is fundamentally based on your parents' existence (parent constructor runs first).
    *   `super.someAdvice()`: Asking your parent for their original advice (`super.method()`) before you add your own take on it (`override`).

---
### **Topic 3: The Constructor Calling Order**

#### **Quick Revision Notes:**

*   **The Golden Rule:** When you create an object of a subclass, the **superclass constructor is always executed first**, followed by the subclass constructor.
*   **The Chain:** This process forms a "constructor chain" that goes all the way up to the top of the hierarchy.
*   **How it Works:** The compiler implicitly inserts a `super()` call as the first line of any constructor that doesn't have an explicit `this()` or `super()` call.

#### **Live Practice Question 1: Constructor Chaining**
Let's predict the output of this code to test our understanding of constructor chaining and the `super` keyword.

**Question:** What will be the output when we create a `Manager` object?

```java
class Employee {
    String employeeType = "Generic";

    public Employee() {
        System.out.println("1. Employee constructor called.");
    }

    public Employee(String type) {
        this.employeeType = type;
        System.out.println("2. Employee parameterized constructor called.");
    }
}

class Manager extends Employee {
    public Manager() {
        // We are explicitly calling the parent's parameterized constructor
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

**Explanation:**
1.  We call `new Manager()`.
2.  The `Manager` constructor starts. Its first line is `super("Salaried")`.
3.  This **explicitly calls the parent's constructor that takes a String**. It does *not* call the no-argument `Employee()` constructor.
4.  The `Employee(String type)` constructor runs, prints its message ("2. ..."), and sets `employeeType` to "Salaried".
5.  Control returns to the `Manager` constructor, which then runs its `println` statement ("3. ...").
6.  Finally, the `mgr.employeeType` is printed, showing the value set by the parent constructor.

---

### **Topic 4: Method Overriding & Dynamic Method Dispatch**

#### **1. Method Overriding**
*   **Quick Description:** A subclass provides its own specific implementation for a method that is already defined in its superclass. The method signature (name, parameters) must be identical.
*   **`@Override` Annotation:** This is a special marker you put above an overridden method. It's not required, but it's a best practice. It tells the compiler, "I intend to override a method." If you make a typo in the method name or parameters, the compiler will give you an error, which is very helpful for catching bugs.

#### **2. Dynamic Method Dispatch**
*   **Quick Description:** This is the engine that powers runtime polymorphism. It's the process where the call to an **overridden method is resolved at runtime**, not compile-time.
*   **How it works:** When you call a method using a superclass reference that points to a subclass object, the **JVM looks at the actual object** to decide which version of the method to run.

*   **Analogy to Remember:** **The Universal Remote Control**
    *   **The Remote (`Vehicle` reference):** A universal remote labeled "Vehicle". It has a `start()` button.
    *   **The Devices (`Car`, `Motorcycle` objects):** You have a `Car` and a `Motorcycle`.
    *   **The Action:** When you point the `Vehicle` remote at the `Car` and press `start()`, it turns the key. When you point the *same remote* at the `Motorcycle` and press `start()`, it kicks the starter. The button is the same, but the action dispatched is different depending on the actual object.

#### **Live Practice Question 2: The `Sound` System**
Let's demonstrate Dynamic Method Dispatch.

**Question:**
1.  Create a base class `Animal` with a `makeSound()` method that prints "The animal makes a generic sound."
2.  Create two subclasses, `Dog` and `Cat`, that extend `Animal`.
3.  **Override** the `makeSound()` method in both subclasses to print "Woof!" and "Meow!", respectively.
4.  Create a `static` method `triggerSound(Animal animal)`. This method will take any `Animal` object and call its `makeSound()` method.
5.  In `main`, create a `Dog` object and a `Cat` object. Pass both of them (one at a time) to the *same* `triggerSound()` method and observe the different outputs.

#### **Live Solution & Explanation**
```java
class Animal {
    public void makeSound() {
        System.out.println("The animal makes a generic sound.");
    }
}

class Dog extends Animal {
    @Override
    public void makeSound() {
        System.out.println("Woof!");
    }
}

class Cat extends Animal {
    @Override
    public void makeSound() {
        System.out.println("Meow!");
    }
}

public class Main {
    // This method is polymorphic. Its behavior changes based on the object it receives.
    public static void triggerSound(Animal animal) {
        System.out.print("Triggering sound for the animal... It says: ");
        // DYNAMIC METHOD DISPATCH:
        // The JVM looks at the actual object 'animal' is pointing to at runtime
        // and calls that object's version of makeSound().
        animal.makeSound();
    }

    public static void main(String[] args) {
        // We use the parent 'Animal' as the reference type.
        // This is a common and powerful practice.
        Animal myDog = new Dog();
        Animal myCat = new Cat();
        Animal genericAnimal = new Animal();

        // Pass different object types to the SAME method.
        triggerSound(myDog);        // Will call Dog's makeSound()
        triggerSound(myCat);        // Will call Cat's makeSound()
        triggerSound(genericAnimal); // Will call the original Animal's makeSound()
    }
}
```
**Explanation:** "Look at the `triggerSound` method. It is incredibly simple and flexible. It doesn't need to know about `Dog` or `Cat`. It only knows about the general `Animal` concept. This means we can add a `Cow` class tomorrow, and the `triggerSound` method will work with it instantly, without any changes. This is the power and elegance of Dynamic Method Dispatch."