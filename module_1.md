Of course. Here is a significantly extended, end-to-end learning module based on your provided content. This guide is designed to be a one-stop resource for these topics, complete with detailed theory, relatable analogies, full program examples, and a comprehensive set of practice questions with solutions.

---
---

## **End-to-End Study Guide: Java Fundamentals & OOP Basics**

**For: B.Tech 2nd Year Students (OOPS with Java)**

### **Module 1: Java Operators**

#### **1. Detailed Description**
Operators are the building blocks of any expression in Java. They are special symbols that instruct the compiler to perform specific operations on one, two, or three *operands* (values or variables). Understanding them is fundamental to writing any meaningful code.

---

#### **2. Arithmetic Operators (`+`, `-`, `*`, `/`, `%`)**

*   **What are they?** These are used for performing standard mathematical calculations.
*   **Why use them?** For any numerical task, from calculating a total price to finding an average score.
*   **Real-World Analogy:** Think of them as the basic functions on a calculator.

**Key Point: Integer vs. Floating-Point Division**
This is a common pitfall for beginners.
*   When you divide two integers, Java performs **integer division**, and the result is an integer (the decimal part is truncated).
*   To get a precise decimal result, at least one of the operands must be a floating-point type (`float` or `double`).

**Program Example:**
```java
public class DivisionExample {
    public static void main(String[] args) {
        // --- Integer Division ---
        int a = 10;
        int b = 3;
        int intResult = a / b;
        System.out.println("Integer Division (10 / 3): " + intResult); // Output: 3

        // --- Floating-Point Division ---
        double c = 10.0;
        double doubleResult = c / b; // double / int -> results in double
        System.out.println("Floating-Point Division (10.0 / 3): " + doubleResult); // Output: 3.333...

        // --- Modulo Operator for finding remainder ---
        int remainder = a % b;
        System.out.println("Remainder (10 % 3): " + remainder); // Output: 1

        // Real-world use of Modulo: Checking for even or odd
        int num = 17;
        if (num % 2 == 0) {
            System.out.println(num + " is Even.");
        } else {
            System.out.println(num + " is Odd."); // This will be printed
        }
    }
}
```

---

#### **3. Relational & Logical Operators**

*   **What are they?**
    *   **Relational (`==`, `!=`, `>`, `<`, `>=`, `<=`):** Compare two values and produce a `boolean` (`true` or `false`) result.
    *   **Logical (`&&`, `||`, `!`):** Combine multiple boolean expressions to form complex conditions.
*   **Why use them?** They are the heart of decision-making in programming, used extensively in `if` statements and loops.
*   **Real-World Analogy:** They are like questions you ask to make a decision. "Is the temperature *greater than* 30°C **AND** is it *not* raining?" Based on the answer, you decide whether to go to the beach.

**Key Point: Short-Circuiting**
*   **`&&` (AND):** If the first operand is `false`, the second operand is **not evaluated** because the entire expression can only be `false`.
*   **`||` (OR):** If the first operand is `true`, the second operand is **not evaluated** because the entire expression can only be `true`.
This is an important optimization feature and can prevent errors (e.g., checking for null before accessing a method).

**Program Example:**
```java
public class LogicExample {
    public static void main(String[] args) {
        int age = 25;
        boolean hasLicense = true;

        // Using && (AND)
        if (age >= 18 && hasLicense) {
            System.out.println("You are eligible to drive."); // Prints
        }

        int marks = 45;
        boolean hasAttendance = false;
        // Using || (OR)
        if (marks > 80 || hasAttendance) {
            System.out.println("Eligible for distinction."); // Does not print
        } else {
            System.out.println("Not eligible for distinction."); // Prints
        }
        
        // Using ! (NOT)
        boolean isLoggedIn = false;
        if (!isLoggedIn) {
            System.out.println("Please log in to continue."); // Prints
        }

        // Short-circuiting example
        String name = null;
        // The second part is NOT evaluated, preventing a NullPointerException
        if (name != null && name.equals("Admin")) {
            System.out.println("Welcome, Admin!");
        } else {
            System.out.println("Guest user or null name."); // Prints
        }
    }
}
```

---

#### **4. Operator Precedence**
Operator precedence defines the "pecking order" of operators. It's the set of rules that determines which operation to perform first in a complex expression. Parentheses `()` can always be used to override the default order.

**Detailed Example Breakdown:**
```java
int x = 10, y = 5;
boolean result = x > y && y * 2 == x || x + y == 15;
// Evaluates to: ( (x > y) && ((y * 2) == x) ) || ( (x + y) == 15 )
```
1.  **Highest Precedence (Multiplication/Addition):**
    *   `y * 2` → `5 * 2` → `10`
    *   `x + y` → `10 + 5` → `15`
    *   Expression becomes: `x > y && 10 == x || 15 == 15`

2.  **Next (Relational Operators):**
    *   `x > y` → `10 > 5` → `true`
    *   `10 == x` → `10 == 10` → `true`
    *   `15 == 15` → `true`
    *   Expression becomes: `true && true || true`

3.  **Next (Logical AND `&&`):**
    *   `true && true` → `true`
    *   Expression becomes: `true || true`

4.  **Last (Logical OR `||`):**
    *   `true || true` → `true`

**Final Result:** `true`

---
---

### **Module 2: Control Flow Statements**

#### **1. Detailed Description**
By default, a program executes statements sequentially. Control flow statements are commands that alter this sequence, allowing the program to make decisions, repeat actions, and jump to other parts of the code. Mastering them is essential for creating dynamic and intelligent applications.

---

#### **2. Selection Statements (`if`, `switch`)**

*   **When to use `if-else-if`:** Best for complex conditions involving ranges or multiple unrelated variables. (e.g., `if (score > 90)`, `if (age > 18 && income > 5000)`).
*   **When to use `switch`:** Best when you are comparing a *single* variable against a list of *discrete, constant* values (integers, strings, enums). It's often cleaner and more efficient than a long `if-else-if` chain for this specific scenario.

**Real-World Example: A Coffee Shop**
An `if-else-if` ladder can handle complex discount logic: "If the order total is > 500 AND the customer is a premium member...". A `switch` statement can handle the simple choice of coffee size: "case 'S': price = 100; case 'M': price = 150...".

**Program Example: ATM Menu**
This is a classic use case for `switch` within a `do-while` loop.
```java
import java.util.Scanner;

public class AtmMachine {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        int choice;
        double balance = 5000.00;

        do {
            System.out.println("\n--- ATM Menu ---");
            System.out.println("1. Check Balance");
            System.out.println("2. Withdraw Money");
            System.out.println("3. Deposit Money");
            System.out.println("4. Exit");
            System.out.print("Enter your choice: ");
            choice = scanner.nextInt();

            switch (choice) {
                case 1:
                    System.out.printf("Your current balance is: ₹%.2f\n", balance);
                    break;
                case 2:
                    System.out.print("Enter amount to withdraw: ");
                    double withdrawAmount = scanner.nextDouble();
                    if (withdrawAmount > balance) {
                        System.out.println("Insufficient funds.");
                    } else {
                        balance -= withdrawAmount;
                        System.out.printf("Withdrawal successful. New balance: ₹%.2f\n", balance);
                    }
                    break;
                case 3:
                    System.out.print("Enter amount to deposit: ");
                    double depositAmount = scanner.nextDouble();
                    balance += depositAmount;
                    System.out.printf("Deposit successful. New balance: ₹%.2f\n", balance);
                    break;
                case 4:
                    System.out.println("Thank you for using our ATM. Goodbye!");
                    break;
                default:
                    System.out.println("Invalid choice. Please try again.");
            }
        } while (choice != 4);
        
        scanner.close();
    }
}
```

---

#### **3. Iteration Statements (`for`, `while`, `do-while`)**

*   **When to use `for`:** When you know the exact start, end, and step for the iterations. Perfect for iterating over arrays or a fixed range.
*   **When to use `while`:** When the loop depends on a condition that can change in unpredictable ways inside the loop. The number of iterations is not known beforehand.
*   **When to use `do-while`:** Exactly like `while`, but you need to guarantee the loop body runs at least once, regardless of the condition. Perfect for "show menu, then process choice" logic.

**Real-World Example: Streaming a Video**
A `for` loop might be used to load the first 10 seconds of video into a buffer (a known number of chunks). A `while` loop would be used for the playback itself: `while (video.isPlaying() && !user.hasPressedStop()) { ... }`.

**Program Example: Number Reversal (using `while`)**
This is a classic problem where the number of iterations depends on the number of digits in the input.
```java
public class ReverseNumber {
    public static void main(String[] args) {
        int number = 12345;
        int reversedNumber = 0;
        int originalNumber = number;

        while (number != 0) {
            int digit = number % 10; // Get the last digit
            reversedNumber = reversedNumber * 10 + digit;
            number /= 10; // Remove the last digit
        }

        System.out.println("Original Number: " + originalNumber);
        System.out.println("Reversed Number: " + reversedNumber);
    }
}
```

---
---

### **Module 3: Methods, CLI & Varargs**

#### **1. Detailed Description: Methods**
Methods (or functions) are the verbs of your program; they encapsulate actions. The most important principle they enable is **DRY (Don't Repeat Yourself)**. If you find yourself writing the same block of code in multiple places, it's a strong signal that you should extract it into a method. This makes your code cleaner, easier to debug (you only fix it in one place), and more maintainable.

**Real-World Example: Making Tea**
Instead of listing the steps "boil water, add tea leaves, add milk, add sugar" every time you want tea, you create a "makeTea" method. Now, you can just call `makeTea()` whenever needed. If you decide to change the recipe (e.g., use honey instead of sugar), you only change it inside the `makeTea` method.

**Program Example:**
```java
public class Utility {
    // A static method, can be called directly using the class name
    public static boolean isValidEmail(String email) {
        if (email == null || email.isEmpty()) {
            return false;
        }
        // A simple check: must contain '@' and '.'
        return email.contains("@") && email.contains(".");
    }

    public static void main(String[] args) {
        String email1 = "test@example.com";
        String email2 = "invalid-email";

        if (Utility.isValidEmail(email1)) {
            System.out.println(email1 + " is a valid email format.");
        }
        if (!Utility.isValidEmail(email2)) {
            System.out.println(email2 + " is NOT a valid email format.");
        }
    }
}
```

---

#### **2. Detailed Description: Command Line Arguments & Varargs**
*   **Command Line Arguments:** This is the primary way to pass initial configuration or data to a standalone application. Professional tools like `git`, `docker`, and `javac` itself are all driven by command-line arguments (e.g., `git clone <url>`, `javac MyFile.java`).
*   **Varargs:** This is purely a convenience feature ("syntactic sugar"). It allows you to create more flexible methods without forcing the user to manually create an array. Internally, the compiler converts the sequence of arguments into an array for you.

**Program Example: Flexible Logger**
```java
public class Logger {
    // A method that takes a mandatory message and optional arguments
    public static void log(String message, Object... args) {
        // String.format replaces {} with the provided arguments
        System.out.println("[LOG]: " + String.format(message, args));
    }

    public static void main(String[] args) {
        String user = "Admin";
        String action = "login";

        // Calling with varargs
        log("User '{}' performed action '{}'.", user, action);
        
        // Calling without varargs
        log("System is starting up.");
        
        // Calling with more varargs
        log("Data processing complete. Processed {} records in {} ms.", 1000, 150.5);
    }
}
```

---
---

### **Module 4: The Pillars of OOP - Classes, Abstract Classes & Interfaces**

#### **1. Detailed Description: Classes and Objects**
*   **Class:** A **blueprint** that defines the structure and behavior for a type of object. It's a logical construct.
*   **Object:** A **physical instance** of a class, residing in memory. Each object has its own state (values for its instance variables) but shares the same behavior (methods) defined by the class.
*   **`new` keyword:** This is the magic wand. When you use `new`, you are telling the JVM to:
    1.  Allocate memory in the **Heap** for a new object.
    2.  Run the **constructor** to initialize the object's state.
    3.  Return a **reference** (memory address) to that new object.

**Program Example: The `Car` Class**
```java
public class Car {
    // --- Attributes (State) ---
    private String model;
    private int year;
    private double currentSpeed;

    // --- Constructor: Special method for creating and initializing objects ---
    public Car(String model, int year) {
        this.model = model;
        this.year = year;
        this.currentSpeed = 0.0; // Default speed is 0
        System.out.println("A new car created: " + year + " " + model);
    }

    // --- Behaviors (Methods) ---
    public void accelerate(double amount) {
        this.currentSpeed += amount;
        System.out.println(this.model + " is now moving at " + this.currentSpeed + " km/h.");
    }

    public void brake() {
        this.currentSpeed = 0.0;
        System.out.println(this.model + " has stopped.");
    }

    public void displayDetails() {
        System.out.println("Car Details - Model: " + this.model + ", Year: " + this.year);
    }
}

// A separate class to run the program
public class Garage {
    public static void main(String[] args) {
        // Creating two distinct car objects from the same class blueprint
        Car car1 = new Car("Honda Civic", 2022);
        Car car2 = new Car("Ford Mustang", 2023);

        car1.displayDetails();
        car2.displayDetails();

        System.out.println("\n--- Driving the cars ---");
        car1.accelerate(60);
        car2.accelerate(100);

        car1.brake();
    }
}
```

---

#### **2. Detailed Description: Abstract Classes**
An abstract class is a blend of specification and implementation. It's used when you want to create a family of related classes that share some common code but must also provide their own unique implementation for certain features. It enforces an **"is-a"** relationship. A `Dog` *is an* `Animal`. A `CreditCardPayment` *is a* `PaymentMethod`.

**Real-World Example: Payment Processing System**
Imagine an e-commerce site that accepts payments via Credit Card, PayPal, and UPI. All these are "Payment Methods". They share common data (like `transactionId`, `amount`) and common behavior (like `validate()`). However, the actual `processPayment()` step is completely different for each. This is a perfect scenario for an abstract class.

**Program Example:**
```java
// File: PaymentMethod.java
public abstract class PaymentMethod {
    protected double amount;

    public void setAmount(double amount) {
        this.amount = amount;
    }

    // A concrete method shared by all subclasses
    public void validate() {
        System.out.println("Validating payment for amount: " + amount);
    }

    // An abstract method - subclasses MUST implement this
    public abstract void processPayment();
}

// File: CreditCardPayment.java
public class CreditCardPayment extends PaymentMethod {
    @Override
    public void processPayment() {
        System.out.println("Processing credit card payment of " + amount + "...");
        // Logic to connect to payment gateway, etc.
        System.out.println("Credit Card Payment Successful.");
    }
}

// File: UpiPayment.java
public class UpiPayment extends PaymentMethod {
    @Override
    public void processPayment() {
        System.out.println("Processing UPI payment of " + amount + "...");
        // Logic to generate QR code or send to VPA
        System.out.println("UPI Payment Successful.");
    }
}

// File: ECommerceSite.java
public class ECommerceSite {
    public static void main(String[] args) {
        // We can't do: new PaymentMethod(); // This would be an error
        
        PaymentMethod ccPayment = new CreditCardPayment();
        ccPayment.setAmount(1500.50);
        ccPayment.validate(); // Calling shared method
        ccPayment.processPayment(); // Calling subclass-specific method

        System.out.println("---");

        PaymentMethod upiPayment = new UpiPayment();
        upiPayment.setAmount(499.00);
        upiPayment.validate();
        upiPayment.processPayment();
    }
}
```

---

#### **3. Detailed Description: Interfaces**
An interface is a pure **contract**. It specifies a set of methods that a class *must* implement. It defines a **"can-do"** relationship or a capability. It doesn't care *what* an object is, only *what it can do*. A `Bird` can fly, an `Airplane` can fly. They are unrelated, but they both share the `Flyable` capability. This is the key to flexible and decoupled software design.

**Real-World Example: Notification Service**
A system needs to send notifications. It could be via Email, SMS, or a Push Notification to a mobile app. By creating a `NotificationService` interface, the main application doesn't need to know the specific details of how a notification is sent. It can just call `service.sendNotification()`. You can easily add a new `WhatsAppNotification` service later without changing the main application code.

**Program Example:**
```java
// File: NotificationService.java
public interface NotificationService {
    // All methods in an interface are public and abstract by default
    void sendNotification(String recipient, String message);
}

// File: EmailService.java
public class EmailService implements NotificationService {
    @Override
    public void sendNotification(String recipient, String message) {
        System.out.println("Sending EMAIL to " + recipient);
        System.out.println("Message: " + message);
        System.out.println("Email sent successfully.");
    }
}

// File: SmsService.java
public class SmsService implements NotificationService {
    @Override
    public void sendNotification(String recipient, String message) {
        System.out.println("Sending SMS to " + recipient);
        System.out.println("Message: " + message);
        System.out.println("SMS sent successfully.");
    }
}

// File: Application.java
public class Application {
    // This method depends on the INTERFACE, not a concrete class
    public static void sendOrderConfirmation(NotificationService service, String customerEmailOrPhone) {
        System.out.println("\n--- Processing Order ---");
        // ... order processing logic ...
        service.sendNotification(customerEmailOrPhone, "Your order #12345 has been confirmed.");
    }

    public static void main(String[] args) {
        // We can easily switch the implementation
        NotificationService emailSender = new EmailService();
        NotificationService smsSender = new SmsService();

        // Send confirmation via Email
        sendOrderConfirmation(emailSender, "customer@example.com");

        // Send confirmation via SMS
        sendOrderConfirmation(smsSender, "+91-9876543210");
    }
}
```

---
---

### **Practice Questions & Solutions**

#### **Section A: Operators & Control Flow**

**Q1. Prime Number Check:** Write a Java program to check if a given integer is a prime number. A prime number is a natural number greater than 1 that has no positive divisors other than 1 and itself.

**Q2. Fibonacci Series:** Write a program to print the Fibonacci series up to a given number `n`. The Fibonacci sequence is a series of numbers where each number is the sum of the two preceding ones, usually starting with 0 and 1. (e.g., for n=10, output is `0, 1, 1, 2, 3, 5, 8`)

**Q3. Login System:** Simulate a user login system. The correct username is "admin" and the password is "pass123". The user has a maximum of 3 attempts. Use a loop and `if-else` conditions. Use `break` to exit the loop on successful login.

---

#### **Section B: Functions, OOP Design & Implementation**

**Q4. Varargs Maximum:** Write a method `findMax` that uses varargs to accept any number of integers and returns the largest one. Handle the case where no numbers are passed (it should return `Integer.MIN_VALUE`).

**Q5. Class Design: `BankAccount`**
Design and implement a `BankAccount` class with the following features:
*   **Attributes (private):** `accountNumber` (String), `accountHolderName` (String), `balance` (double).
*   **Encapsulation:** Protect the attributes and provide public getter methods for all of them. `balance` should not have a public setter.
*   **Constructor:** A constructor to initialize the account number and holder name. The initial balance should be set to 0.
*   **Methods:**
    *   `deposit(double amount)`: Adds the amount to the balance. Should not allow negative amounts.
    *   `withdraw(double amount)`: Subtracts the amount from the balance. Should not allow withdrawal if the amount is greater than the balance.
    *   `displayBalance()`: Prints the current balance.

**Q6. Advanced Design: `Shape` Hierarchy**
Design a system for calculating the area of different shapes.
1.  Create an `abstract class` named `Shape` with an `abstract method` `calculateArea()` that returns a `double`. It should also have a concrete method `display()` that prints "Displaying a shape.".
2.  Create two concrete classes, `Circle` (with a `radius` attribute) and `Rectangle` (with `width` and `height` attributes), that `extend` the `Shape` class. Implement the `calculateArea()` method in both.
3.  In a `main` method, create objects of `Circle` and `Rectangle` and demonstrate polymorphism by calling their methods through a `Shape` reference.

---
---

### **Solutions to Practice Questions**

#### **Solution A1: Prime Number Check**
```java
public class PrimeCheck {
    public static void main(String[] args) {
        int num = 29; // Number to check
        boolean isPrime = true;

        if (num <= 1) {
            isPrime = false;
        } else {
            for (int i = 2; i <= Math.sqrt(num); i++) {
                if (num % i == 0) {
                    isPrime = false;
                    break; // No need to check further
                }
            }
        }

        if (isPrime) {
            System.out.println(num + " is a prime number.");
        } else {
            System.out.println(num + " is not a prime number.");
        }
    }
}
```

---

#### **Solution A2: Fibonacci Series**
```java
public class Fibonacci {
    public static void main(String[] args) {
        int n = 10; // Number of terms to print
        int t1 = 0, t2 = 1;

        System.out.print("Fibonacci Series up to " + n + " terms: ");
        for (int i = 1; i <= n; ++i) {
            System.out.print(t1 + " ");
            int sum = t1 + t2;
            t1 = t2;
            t2 = sum;
        }
    }
}
```

---

#### **Solution A3: Login System**
```java
import java.util.Scanner;
public class LoginSystem {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        int attempts = 0;
        final int MAX_ATTEMPTS = 3;
        boolean loggedIn = false;

        while (attempts < MAX_ATTEMPTS) {
            System.out.print("Enter username: ");
            String username = scanner.nextLine();
            System.out.print("Enter password: ");
            String password = scanner.nextLine();

            if (username.equals("admin") && password.equals("pass123")) {
                System.out.println("Login successful! Welcome, admin.");
                loggedIn = true;
                break; // Exit the loop
            } else {
                attempts++;
                System.out.println("Invalid credentials. You have " + (MAX_ATTEMPTS - attempts) + " attempts left.");
            }
        }

        if (!loggedIn) {
            System.out.println("You have exceeded the maximum number of attempts. Account locked.");
        }
        scanner.close();
    }
}
```

---

#### **Solution B4: Varargs Maximum**
```java
public class VarargsMax {
    public static int findMax(int... numbers) {
        if (numbers.length == 0) {
            return Integer.MIN_VALUE; // Sentinel value for no input
        }

        int max = numbers[0];
        for (int i = 1; i < numbers.length; i++) {
            if (numbers[i] > max) {
                max = numbers[i];
            }
        }
        return max;
    }

    public static void main(String[] args) {
        System.out.println("Max of (3, 5, 1, 9, 4): " + findMax(3, 5, 1, 9, 4));
        System.out.println("Max of (-10, -5, -20): " + findMax(-10, -5, -20));
        System.out.println("Max of (100): " + findMax(100));
        System.out.println("Max of no numbers: " + findMax());
    }
}
```

---

#### **Solution B5: `BankAccount` Class**
```java
public class BankAccount {
    private String accountNumber;
    private String accountHolderName;
    private double balance;

    public BankAccount(String accountNumber, String accountHolderName) {
        this.accountNumber = accountNumber;
        this.accountHolderName = accountHolderName;
        this.balance = 0.0;
    }

    public String getAccountNumber() { return accountNumber; }
    public String getAccountHolderName() { return accountHolderName; }
    public double getBalance() { return balance; }

    public void deposit(double amount) {
        if (amount > 0) {
            this.balance += amount;
            System.out.println("Successfully deposited: " + amount);
        } else {
            System.out.println("Deposit amount must be positive.");
        }
    }

    public void withdraw(double amount) {
        if (amount > this.balance) {
            System.out.println("Withdrawal failed. Insufficient funds.");
        } else if (amount <= 0) {
            System.out.println("Withdrawal amount must be positive.");
        } else {
            this.balance -= amount;
            System.out.println("Successfully withdrew: " + amount);
        }
    }

    public void displayBalance() {
        System.out.printf("Account [%s] Balance: ₹%.2f\n", this.accountNumber, this.balance);
    }

    // Main method for testing
    public static void main(String[] args) {
        BankAccount myAccount = new BankAccount("123456789", "Anjali Sharma");
        myAccount.displayBalance();
        myAccount.deposit(5000);
        myAccount.displayBalance();
        myAccount.withdraw(2000);
        myAccount.displayBalance();
        myAccount.withdraw(4000); // This will fail
        myAccount.displayBalance();
    }
}
```

---

#### **Solution B6: `Shape` Hierarchy**
```java
// File: Shape.java
abstract class Shape {
    public abstract double calculateArea();

    public void display() {
        System.out.println("Displaying a shape.");
    }
}

// File: Circle.java
class Circle extends Shape {
    private double radius;
    public Circle(double radius) { this.radius = radius; }
    @Override
    public double calculateArea() {
        return Math.PI * radius * radius;
    }
}

// File: Rectangle.java
class Rectangle extends Shape {
    private double width;
    private double height;
    public Rectangle(double width, double height) {
        this.width = width;
        this.height = height;
    }
    @Override
    public double calculateArea() {
        return width * height;
    }
}

// File: ShapeDemo.java
public class ShapeDemo {
    public static void main(String[] args) {
        // Polymorphism in action
        Shape shape1 = new Circle(5.0);
        Shape shape2 = new Rectangle(4.0, 6.0);

        // --- Demonstrating for Circle ---
        shape1.display(); // Calls method from Shape class
        System.out.printf("Area of the circle is: %.2f\n", shape1.calculateArea());

        System.out.println("\n--- Demonstrating for Rectangle ---");
        // --- Demonstrating for Rectangle ---
        shape2.display();
        System.out.printf("Area of the rectangle is: %.2f\n", shape2.calculateArea());
    }
}
```