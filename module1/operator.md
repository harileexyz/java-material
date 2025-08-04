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
