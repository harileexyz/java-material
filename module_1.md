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
---

### **In-Depth Look: Operator Precedence in Java**

#### **1. What is Operator Precedence? A Deeper Dive**

Think of operator precedence as the "rules of grammar" for mathematical and logical expressions in Java. Just as English grammar dictates the order and meaning of words in a sentence, operator precedence dictates the order in which operations are performed in an expression.

Without these rules, a simple expression like `3 + 5 * 2` would be ambiguous.
*   Does it mean `(3 + 5) * 2` which equals `16`?
*   Or does it mean `3 + (5 * 2)` which equals `13`?

To ensure that every Java compiler and virtual machine in the world gets the exact same, predictable result, the language defines a strict hierarchy. In Java's case, multiplication has a higher precedence than addition, so the answer is always **13**. This predictability is fundamental to writing reliable software.

**The Golden Rule: When in Doubt, Use Parentheses `()`**
Parentheses have the highest precedence. They are your most powerful tool to control the order of evaluation. Even if you know the precedence rules, using parentheses makes your code **unambiguous and infinitely more readable** for other developers (and your future self!).

`int result = 3 + (5 * 2);` // This is much clearer than relying on implicit precedence.

#### **2. The Precedence and Associativity Table (Simplified)**

Here is a simplified but practical table of precedence for the most common operators, from highest to lowest. **Associativity** determines the order for operators at the *same* precedence level.

| Precedence Level | Category              | Operators               | Associativity |
| :--------------- | :-------------------- | :---------------------- | :------------ |
| 1 (Highest)      | Parentheses           | `()`                    | N/A           |
| 2                | Unary                 | `++` `--` `!` `+` `-` (unary) | Right-to-Left |
| 3                | Multiplicative        | `*` `/` `%`             | Left-to-Right |
| 4                | Additive              | `+` `-`                 | Left-to-Right |
| 5                | Relational            | `<` `>` `<=` `>=` `instanceof` | Left-to-Right |
| 6                | Equality              | `==` `!=`               | Left-to-Right |
| 7                | Logical AND           | `&&`                    | Left-to-Right |
| 8                | Logical OR            | `||`                    | Left-to-Right |
| 9                | Ternary               | `? :`                   | Right-to-Left |
| 10 (Lowest)      | Assignment            | `=` `+=` `-=` `*=` `/=` | Right-to-Left |

*   **Left-to-Right Associativity:** `10 - 5 + 2` is evaluated as `(10 - 5) + 2`.
*   **Right-to-Left Associativity:** `a = b = c` is evaluated as `a = (b = c)`.

---

### **Step-by-Step Examples**

Let's break down several examples, from simple to complex, to see these rules in action.

#### **Example 1: Basic Arithmetic Precedence**

**The Code:**
```java
int result = 10 + 20 / 5 * 2 - 3;
```
**The Question:** What is the value of `result`?

**Step-by-Step Breakdown:**
1.  The expression has `+`, `/`, `*`, and `-`.
2.  Looking at the table, Multiplicative operators (`*`, `/`) have higher precedence than Additive operators (`+`, `-`).
3.  Since `*` and `/` are at the same level, we use their **Left-to-Right** associativity.
4.  **Step 1 (Division):** The first multiplicative operator from the left is `/`.
    *   `20 / 5` evaluates to `4`.
    *   Expression becomes: `10 + 4 * 2 - 3`
5.  **Step 2 (Multiplication):** The next multiplicative operator is `*`.
    *   `4 * 2` evaluates to `8`.
    *   Expression becomes: `10 + 8 - 3`
6.  Now, we are left with `+` and `-`, which are at the same level. We use their **Left-to-Right** associativity.
7.  **Step 3 (Addition):** The first additive operator from the left is `+`.
    *   `10 + 8` evaluates to `18`.
    *   Expression becomes: `18 - 3`
8.  **Step 4 (Subtraction):**
    *   `18 - 3` evaluates to `15`.

**Final Result:** `15`

---

#### **Example 2: The Power of Parentheses**

**The Code:**
```java
// Same expression as above, but with parentheses
int result = (10 + 20) / 5 * 2 - 3;
```
**The Question:** How do the parentheses change the outcome?

**Step-by-Step Breakdown:**
1.  **Step 1 (Parentheses):** Parentheses have the highest precedence. We evaluate the expression inside them first.
    *   `10 + 20` evaluates to `30`.
    *   Expression becomes: `30 / 5 * 2 - 3`
2.  Now we follow the same rules as in Example 1. Multiplicative (`/`, `*`) before Additive (`-`).
3.  **Step 2 (Division):** Using Left-to-Right associativity for `*` and `/`.
    *   `30 / 5` evaluates to `6`.
    *   Expression becomes: `6 * 2 - 3`
4.  **Step 3 (Multiplication):**
    *   `6 * 2` evaluates to `12`.
    *   Expression becomes: `12 - 3`
5.  **Step 4 (Subtraction):**
    *   `12 - 3` evaluates to `9`.

**Final Result:** `9` (A completely different result, highlighting the importance of parentheses!)

---

#### **Example 3: Combined Relational and Logical Operators (Your Original Example)**

**The Code:**
```java
int x = 10, y = 5;
boolean result = x > y && y * 2 == x || x + y == 15;
```
**The Question:** What is the boolean value of `result`?

**Step-by-Step Breakdown:**
1.  **Highest Precedence (Arithmetic):** `*` and `+` are evaluated first.
    *   `y * 2` → `5 * 2` → `10`
    *   `x + y` → `10 + 5` → `15`
    *   Expression becomes: `x > y && 10 == x || 15 == 15`
2.  **Next (Relational Operators):** `>`, `==` have higher precedence than `&&` and `||`.
    *   `x > y` → `10 > 5` → `true`
    *   `10 == x` → `10 == 10` → `true`
    *   `15 == 15` → `true`
    *   Expression becomes: `true && true || true`
3.  **Next (Logical AND `&&`):** `&&` has higher precedence than `||`.
    *   `true && true` → `true`
    *   Expression becomes: `true || true`
4.  **Last (Logical OR `||`):**
    *   `true || true` → `true`

**Final Result:** `true`

---

#### **Example 4: Compound Assignment Operators**

This is a common point of confusion. The entire right-hand side of an assignment operator is evaluated *before* the assignment takes place.

**The Code:**
```java
int a = 5;
a *= 2 + 3; // This is equivalent to a = a * (2 + 3);
```
**The Question:** What is the final value of `a`?

**Step-by-Step Breakdown:**
1.  **Rule:** The expression on the right-hand side (`2 + 3`) is evaluated first.
2.  **Step 1 (Addition):**
    *   `2 + 3` evaluates to `5`.
    *   The statement is now effectively `a *= 5;`
3.  **Step 2 (Compound Assignment):** This is executed as `a = a * 5`.
    *   `a = 5 * 5`
    *   `a` becomes `25`.

**Final Result:** `25` (A common mistake is to calculate `5 * 2` first, which would yield 13).

---

#### **Example 5: The "Tricky" Unary and Short-Circuiting Example**

This example combines unary operators (`++`), which have high precedence, with logical operators, which can short-circuit.

**The Code:**
```java
int x = 5, y = 10;
// Note: x++ (post-increment) vs ++y (pre-increment)
boolean result = x++ < 5 && ++y > 10;
System.out.println("Result: " + result);
System.out.println("Final x: " + x);
System.out.println("Final y: " + y);
```
**The Question:** What are the final values of `result`, `x`, and `y`?

**Step-by-Step Breakdown:**
1.  The `&&` operator is evaluated from left to right.
2.  **Evaluate the left side:** `x++ < 5`
    *   This is a **post-increment**. The *original value* of `x` (which is 5) is used for the comparison first.
    *   The comparison is `5 < 5`, which is **`false`**.
    *   *After* the comparison, `x` is incremented to `6`.
3.  **Short-Circuiting in Action:** The expression is now `false && ...`.
    *   Since the left-hand side of a logical AND (`&&`) is `false`, the entire expression *must* be `false`, regardless of what the right-hand side is.
    *   Java is smart and **skips the evaluation of the right-hand side (`++y > 10`) completely**.
4.  **Final Assignments:**
    *   `result` is assigned the value `false`.
    *   `x` became `6` in step 2.
    *   `y` was **never touched** because its part of the expression was skipped. It remains `10`.

**Final Result:**
```
Result: false
Final x: 6
Final y: 10
```

---
---

### **In-Depth Look: Control Flow Statements in Java**

#### **1. Detailed Description**

Imagine a program's code as a straight road. By default, the computer starts at the beginning and drives straight to the end, executing every instruction in order. Control Flow Statements are like the road signs, traffic lights, and roundabouts on this road. They give you the power to direct the flow of execution.
*   **Decisions (`if`, `switch`):** These are the forks in the road. "If the weather is sunny, turn left to the beach; otherwise, turn right to the mall."
*   **Repetition (`for`, `while`):** These are the loops or laps on a racetrack. "Keep running laps until you've completed 5 miles."
*   **Jumps (`break`, `continue`):** These are the emergency exits or shortcuts. "If you get a flat tire, `break` out of the race. If you just need a water break, `continue` to the next lap after you're done."

Without control flow, programs would be incredibly limited, only able to perform a single, fixed sequence of tasks. Mastering control flow is what allows you to build applications that are responsive, intelligent, and useful.

---

### **2. Selection Statements: `if` vs. `switch`**

#### **`if-else-if` Ladder: The Flexible Decision-Maker**

The `if-else-if` structure is the most versatile tool for decision-making. It evaluates a series of conditions sequentially until one is found to be `true`. Once a condition is met, its corresponding block is executed, and the rest of the chain is skipped.

*   **Strength:** It can handle any type of boolean expression, including range checks (`score > 90`), compound logic (`age > 18 && hasLicense`), and method calls (`user.isAdmin()`).
*   **Anatomy:**
    *   `if (...)`: The first check. Mandatory.
    *   `else if (...)`: Zero or more optional, subsequent checks.
    *   `else`: An optional "catch-all" block that runs if no preceding condition was true.

**Real-World Example: Grading System**
A grading system is a perfect example of mutually exclusive ranges, making it ideal for `if-else-if`.

```java
public class Grader {
    public static void main(String[] args) {
        int score = 78;
        char grade;

        if (score >= 90) {
            grade = 'A';
        } else if (score >= 80) {
            grade = 'B';
        } else if (score >= 70) {
            grade = 'C';
        } else if (score >= 60) {
            grade = 'D';
        } else {
            grade = 'F';
        }

        System.out.println("A score of " + score + " earns a grade of: " + grade); // Prints 'C'
    }
}
```

---

#### **`switch` Statement: The Efficient Specialist**

The `switch` statement is a specialized tool for comparing a single variable against a list of discrete, constant values. Behind the scenes, the compiler can often optimize a `switch` statement into more efficient bytecode than a long `if-else-if` chain, making it faster for certain scenarios.

*   **Strength:** Clean, readable, and efficient for handling a fixed set of choices like menu options, error codes, or user roles.
*   **Anatomy:**
    *   `switch (variable)`: The variable to be tested. Can be `byte`, `short`, `char`, `int`, `String` (since Java 7), or an `enum`.
    *   `case value:`: A specific constant value to compare against.
    *   `break;`: **Crucial!** This keyword exits the `switch` block. Without it, execution "falls through" to the next `case`.
    *   `default:`: An optional block that runs if no `case` matches. It's like the final `else`.

**Common Pitfall: The Missing `break` (Fall-through Behavior)**
This is a frequent source of bugs. If you forget `break`, the program will execute the code for the matching `case` and then continue executing the code for all subsequent `cases` until it hits a `break` or the end of the `switch` block. Sometimes this is intentional, but usually, it's an error.

**Example Demonstrating Fall-through:**
```java
public class DayTypeIdentifier {
    public static void main(String[] args) {
        int day = 6; // Saturday
        String dayType;

        // Using intentional fall-through for grouping cases
        switch (day) {
            case 1:
            case 2:
            case 3:
            case 4:
            case 5:
                dayType = "Weekday";
                break; // Exit after setting to "Weekday"
            case 6:
            case 7:
                dayType = "Weekend";
                break; // Exit after setting to "Weekend"
            default:
                dayType = "Invalid Day";
                break;
        }
        System.out.println("Day " + day + " is a " + dayType); // Prints "Weekend"
    }
}
```
In the example above, if `day` is 2, it matches `case 2:`. Since there's no code or `break` there, it "falls through" until it hits the code under `case 5:`, sets `dayType` to "Weekday", and then breaks. This is a powerful way to group related cases.

---

### **3. Iteration Statements: `for`, `while`, and `do-while`**

#### **The `for` Loop: The Determinate Iterator**

The `for` loop is your go-to when you know exactly how many times you need to repeat a task. Its structure is explicitly designed for count-controlled loops.

*   **Anatomy:** `for (initialization; condition; update)`
    *   **Initialization:** Runs *once* at the very beginning. Used to declare and initialize a loop control variable (e.g., `int i = 0`).
    *   **Condition:** Checked *before* each iteration. If `true`, the loop body executes. If `false`, the loop terminates.
    *   **Update:** Runs *after* each iteration. Used to modify the loop control variable (e.g., `i++`, `i--`, `i += 2`).

**Real-World Example: Printing a Calendar Month**
You know a month like January has exactly 31 days. A `for` loop is perfect for this: `for (int day = 1; day <= 31; day++)`.

**Program Example: Generating a Multiplication Table**
```java
public class MultiplicationTable {
    public static void main(String[] args) {
        int number = 7;
        System.out.println("--- Multiplication Table for " + number + " ---");

        // The loop runs exactly 10 times, from i=1 to i=10
        for (int i = 1; i <= 10; i++) {
            // printf is used for formatted string output
            // %d is a placeholder for an integer, \n is a newline
            System.out.printf("%d x %d = %d\n", number, i, number * i);
        }
    }
}
```

---

#### **The `while` Loop: The Indeterminate Watcher**

The `while` loop is used when a loop must continue as long as a certain condition remains true, but you don't know in advance when that condition will become false.

*   **Anatomy:** `while (condition)`
    *   **Condition:** Checked *before* each iteration. If `true`, the loop body executes.
*   **Critical Responsibility:** You must ensure that something *inside* the loop's body will eventually make the condition `false`. Otherwise, you will create an **infinite loop**.

**Real-World Example: Game Loop**
A video game's main loop is a `while` loop: `while (gameIsRunning) { processInput(); updateGameLogic(); renderGraphics(); }`. The loop continues indefinitely until the user quits, which sets `gameIsRunning` to `false`.

**Program Example: User Input Validation**
This example keeps asking the user for input until they provide a valid number within a specific range. The number of attempts is unknown.

```java
import java.util.Scanner;

public class InputValidator {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        int number = -1; // Initialize to a value that fails the condition

        // The loop continues as long as the number is outside the valid range
        while (number < 1 || number > 10) {
            System.out.print("Please enter a number between 1 and 10: ");
            number = scanner.nextInt();
        }

        System.out.println("Thank you! You entered a valid number: " + number);
        scanner.close();
    }
}
```

---

#### **The `do-while` Loop: The "Do First, Ask Later" Loop**

The `do-while` loop is a variant of the `while` loop where the condition is checked *at the end* of the loop's body. This provides a guarantee that the loop will execute **at least once**.

*   **Anatomy:** `do { ... } while (condition);`
*   **Strength:** Perfect for scenarios where you need to perform an action and then decide whether to repeat it, such as displaying a menu. The ATM example from earlier is a prime use case.

**Real-World Analogy: Free Sample at a Store**
You get to try the sample (`do` the action) *before* they check if you want to buy more (`while` condition). You are guaranteed to get at least one sample.

**Program Example: A Simple Guessing Game**
The player must be allowed to make at least one guess.

```java
import java.util.Scanner;
import java.util.Random;

public class GuessingGame {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        Random random = new Random();
        int numberToGuess = random.nextInt(100) + 1; // A random number between 1 and 100
        int userGuess;

        System.out.println("I'm thinking of a number between 1 and 100. Can you guess it?");

        do {
            System.out.print("Enter your guess: ");
            userGuess = scanner.nextInt();

            if (userGuess > numberToGuess) {
                System.out.println("Too high! Try again.");
            } else if (userGuess < numberToGuess) {
                System.out.println("Too low! Try again.");
            }

        } while (userGuess != numberToGuess); // Loop continues until the guess is correct

        System.out.println("Congratulations! You guessed the number: " + numberToGuess);
        scanner.close();
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