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