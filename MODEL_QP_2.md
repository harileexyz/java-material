You're absolutely right. An exam preparation guide should be complete. My apologies for skipping those. Here are the detailed answers for the remaining project-based questions, broken down into two parts for clarity as requested.

---
---

### **PART B (Continued)**

### **Module 3: Design Patterns**

**Question 13:**
> You have a third-party class `AnalyticsService` with method `sendEvent(String)`. Write an Adapter so that it conforms to your `Logger` interface (`log(String)`). Show both class definitions and the adapter code.

**Answer:**
This problem requires the **Adapter Design Pattern**. We will create an adapter class that "wraps" the incompatible `AnalyticsService` and makes it usable through our application's standard `Logger` interface.

**Step 1: Define the Target Interface and the Incompatible Class**
```java
// Our application's standard interface for logging. This is the "target".
interface Logger {
    void log(String message);
}

// The third-party class we are given. We cannot change its code.
// This is the "adaptee". Notice its method is named 'sendEvent', not 'log'.
class AnalyticsService {
    public void sendEvent(String eventData) {
        System.out.println("Analytics Service: Sending event -> " + eventData);
    }
}
```

**Step 2: Implement the Adapter Class**
The `AnalyticsAdapter` will implement our `Logger` interface and hold an instance of the `AnalyticsService`. Its `log` method will translate the call to the `sendEvent` method.
```java
// The Adapter class. It makes the AnalyticsService look like a Logger.
class AnalyticsAdapter implements Logger {
    private AnalyticsService analyticsService;

    // The adapter takes the incompatible object in its constructor.
    public AnalyticsAdapter(AnalyticsService service) {
        this.analyticsService = service;
    }

    // This is the core of the adapter. It translates the 'log' call
    // into a 'sendEvent' call on the wrapped object.
    @Override
    public void log(String message) {
        analyticsService.sendEvent(message);
    }
}
```

**Step 3: Demonstrate the Solution in `main`**
The `main` method shows that our application can now use the `AnalyticsService` through the adapter, without knowing any details about the `sendEvent` method.
```java
public class Main {
    public static void main(String[] args) {
        // Our application's logging client. It only knows how to work with the Logger interface.
        class LogClient {
            public void doWork(Logger logger, String data) {
                System.out.println("Client is doing work with data: " + data);
                logger.log("Work completed with data: " + data);
            }
        }
        
        LogClient client = new LogClient();
        AnalyticsService thirdPartyAnalytics = new AnalyticsService();

        // We can't pass the thirdPartyAnalytics object directly to our client:
        // client.doWork(thirdPartyAnalytics, "test"); // COMPILE ERROR!

        // So, we create an adapter.
        Logger adapter = new AnalyticsAdapter(thirdPartyAnalytics);

        // Now, we can pass the adapter to our client. The client thinks it's a regular Logger.
        client.doWork(adapter, "User Login Event");
    }
}
```
**Combined Code for Testing:**
```java
interface Logger { void log(String message); }
class AnalyticsService {
    public void sendEvent(String eventData) {
        System.out.println("Analytics Service: Sending event -> " + eventData);
    }
}
class AnalyticsAdapter implements Logger {
    private AnalyticsService analyticsService;
    public AnalyticsAdapter(AnalyticsService service) { this.analyticsService = service; }
    @Override
    public void log(String message) { analyticsService.sendEvent(message); }
}
public class Main {
    public static void main(String[] args) {
        class LogClient {
            public void doWork(Logger logger, String data) {
                System.out.println("Client is doing work with data: " + data);
                logger.log("Work completed with data: " + data);
            }
        }
        LogClient client = new LogClient();
        AnalyticsService thirdPartyAnalytics = new AnalyticsService();
        Logger adapter = new AnalyticsAdapter(thirdPartyAnalytics);
        client.doWork(adapter, "User Login Event");
    }
}
```

---

**Question 14:**
> Implement the Singleton pattern for a `Logger` class that writes log entries to a file. Show your code and explain how it ensures a single instance.

**Answer:**
The Singleton pattern is used to ensure that a class has only one instance and provides a global point of access to it. This is ideal for a `Logger` to prevent multiple objects from trying to write to the same file simultaneously.

**The code ensures a single instance using three key mechanisms:**
1.  **A `private static` instance variable:** `private static Logger instance;` holds the single object.
2.  **A `private` constructor:** `private Logger() {}` prevents other classes from creating new instances with `new Logger()`.
3.  **A `public static getInstance()` method:** This is the only way to get the `Logger` object. It creates the object the first time it's called and returns that same object on all subsequent calls.

**Implementation:**
```java
import java.io.FileWriter;
import java.io.IOException;
import java.io.PrintWriter;
import java.time.LocalDateTime;

public class Logger {
    // 1. The single, static instance of the Logger.
    private static Logger instance;
    private PrintWriter writer;

    // 2. The private constructor to prevent outside instantiation.
    private Logger() {
        try {
            // In a real app, you would append to the file.
            FileWriter fw = new FileWriter("application.log");
            writer = new PrintWriter(fw, true); // 'true' for auto-flushing
            System.out.println("Logger instance created. Logging to application.log");
        } catch (IOException e) {
            // In a real app, handle this more gracefully.
            e.printStackTrace();
        }
    }

    // 3. The global access point to the single instance.
    public static Logger getInstance() {
        // "Lazy initialization": create the instance only when first needed.
        if (instance == null) {
            instance = new Logger();
        }
        return instance;
    }

    // A method to use the logger.
    public void log(String message) {
        if (writer != null) {
            writer.println(LocalDateTime.now() + ": " + message);
        }
    }

    // Main method to demonstrate its usage.
    public static void main(String[] args) {
        System.out.println("--- Application Start ---");
        
        // Module 1 gets the logger and logs a message.
        Logger logger1 = Logger.getInstance();
        logger1.log("User authentication module started.");
        
        // Module 2 gets the logger and logs another message.
        Logger logger2 = Logger.getInstance();
        logger2.log("Database connection established.");

        // Verification
        if (logger1 == logger2) {
            System.out.println("Verification successful: Both logger1 and logger2 refer to the same object.");
        } else {
            System.out.println("Error: Singleton pattern failed.");
        }
        System.out.println("--- Application End ---");
    }
}
```
*After running this code, an `application.log` file will be created in the project directory with the logged messages, demonstrating that both parts of the application used the same logger instance.*

---
---

### **Module 4 & 5: Swing and JDBC Application**

**Question 15:**
> a) Design a simple Java Swing GUI application with... a "Greet" and "Clear" button...
> b) In your Swing GUI, the user enters a name and clicks ‘Save’. Write the JDBC code to insert that name into table `greetings(name VARCHAR)`, handling exceptions appropriately.

**Answer:**
*(Note: For an exam, you might be asked for either part (a) or part (b), or a combined version. This answer combines both requirements into a single, complete application.)*

This program demonstrates a Swing GUI with event handling for two buttons and includes a JDBC operation to save data to a database.

**Complete Code for the Application:**
```java
import javax.swing.*;
import java.awt.*;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.PreparedStatement;
import java.sql.SQLException;

public class GreeterApp {
    // --- JDBC Connection Details ---
    private static final String DB_URL = "jdbc:mysql://localhost:3306/mydatabase"; // Change mydatabase if needed
    private static final String DB_USER = "root"; // Change to your username
    private static final String DB_PASSWORD = "password"; // Change to your password

    public static void main(String[] args) {
        // --- GUI Setup ---
        JFrame frame = new JFrame("Greeter App");
        frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        frame.setSize(400, 200);
        frame.setLayout(new FlowLayout(FlowLayout.CENTER, 10, 20));

        JTextField nameField = new JTextField(15);
        JButton greetButton = new JButton("Greet");
        JButton clearButton = new JButton("Clear");
        JButton saveButton = new JButton("Save to DB");
        JLabel resultLabel = new JLabel("Enter your name and click a button.");

        frame.add(new JLabel("Name:"));
        frame.add(nameField);
        frame.add(greetButton);
        frame.add(clearButton);
        frame.add(saveButton);
        frame.add(resultLabel);

        // --- Event Handling for "Greet" Button ---
        greetButton.addActionListener(new ActionListener() {
            @Override
            public void actionPerformed(ActionEvent e) {
                String name = nameField.getText();
                if (name.isEmpty()) {
                    resultLabel.setText("Please enter a name first!");
                } else {
                    resultLabel.setText("Hello, " + name + "!");
                }
            }
        });

        // --- Event Handling for "Clear" Button ---
        clearButton.addActionListener(new ActionListener() {
            @Override
            public void actionPerformed(ActionEvent e) {
                nameField.setText("");
                resultLabel.setText("Enter your name and click a button.");
            }
        });
        
        // --- Event Handling for "Save to DB" Button (JDBC Part) ---
        saveButton.addActionListener(new ActionListener() {
            @Override
            public void actionPerformed(ActionEvent e) {
                String name = nameField.getText();
                if (name.isEmpty()) {
                    JOptionPane.showMessageDialog(frame, "Name cannot be empty to save.", "Error", JOptionPane.ERROR_MESSAGE);
                    return;
                }

                // JDBC Code to insert the name
                String sql = "INSERT INTO greetings (name) VALUES (?)";
                try (Connection conn = DriverManager.getConnection(DB_URL, DB_USER, DB_PASSWORD);
                     PreparedStatement pstmt = conn.prepareStatement(sql)) {
                    
                    pstmt.setString(1, name);
                    int rowsAffected = pstmt.executeUpdate();

                    if (rowsAffected > 0) {
                        JOptionPane.showMessageDialog(frame, "Name '" + name + "' saved to database successfully!");
                    }

                } catch (SQLException ex) {
                    // Handle potential database errors gracefully
                    JOptionPane.showMessageDialog(frame, "Database error: " + ex.getMessage(), "Error", JOptionPane.ERROR_MESSAGE);
                    ex.printStackTrace();
                }
            }
        });

        frame.setVisible(true);
    }
}
```
*(Before running, ensure a database `mydatabase` and a table `CREATE TABLE greetings (name VARCHAR(100));` exist.)*

---

Of course. Here is a complete, detailed answer for Question 16(b), including a formal definition of the Dependency Inversion Principle and the full, refactored code to demonstrate its application for unit testing.

---
---

**Question 16 (b):**
> Describe how you’d apply Dependency Inversion so the Controller can be unit-tested without a real database.

### **Answer**

#### **1. Definition of the Dependency Inversion Principle (DIP)**

The Dependency Inversion Principle is one of the five SOLID principles of Object-Oriented Design. It states two things:

1.  **High-level modules should not depend on low-level modules. Both should depend on abstractions (e.g., interfaces).**
2.  **Abstractions should not depend on details. Details (concrete implementations) should depend on abstractions.**

**In simpler terms:** Don't let your important business logic (high-level module, like a controller) be tightly coupled to specific, concrete implementation details (low-level module, like a `MySQLDatabase` class). Instead, make your business logic depend on an interface. This "inverts" the dependency—instead of `High-level -> Low-level`, the relationship becomes `High-level -> Interface <- Low-level`.

This decoupling allows you to easily swap out the low-level implementation (e.g., from a real database to a mock database for testing) without changing the high-level module at all.

#### **2. Applying Dependency Inversion to the GreeterApp**

To make our Swing `ActionListener` (the Controller) unit-testable without a real database, we will apply DIP in three steps:

**Step 1: Create an Abstraction (Interface)**
First, we define an interface that represents the "contract" for what our data storage mechanism must be able to do. This is our abstraction.

```java
// File: GreetingRepository.java
import java.sql.SQLException;

/**
 * An interface that defines the contract for saving greetings.
 * This is our ABSTRACTION.
 */
public interface GreetingRepository {
    void saveName(String name) throws SQLException;
}
```

**Step 2: Create Concrete Implementations (The Details)**
Next, we create concrete classes that "depend on the abstraction" by implementing the interface.

**a) The Real Database Implementation:** This class contains the actual JDBC code.

```java
// File: JdbcGreetingRepository.java
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.PreparedStatement;
import java.sql.SQLException;

/**
 * A concrete implementation that saves data to a real MySQL database.
 * This is a LOW-LEVEL DETAIL.
 */
public class JdbcGreetingRepository implements GreetingRepository {
    private static final String DB_URL = "jdbc:mysql://localhost:3306/mydatabase";
    private static final String DB_USER = "root";
    private static final String DB_PASSWORD = "password";

    @Override
    public void saveName(String name) throws SQLException {
        String sql = "INSERT INTO greetings (name) VALUES (?)";
        try (Connection conn = DriverManager.getConnection(DB_URL, DB_USER, DB_PASSWORD);
             PreparedStatement pstmt = conn.prepareStatement(sql)) {
            
            pstmt.setString(1, name);
            pstmt.executeUpdate();
        }
    }
}
```

**b) The Mock Implementation for Testing:** This "fake" class implements the same interface but doesn't connect to a database. It's used for unit testing.

```java
// File: MockGreetingRepository.java

import java.sql.SQLException;

/**
 * A "mock" implementation for testing purposes. It does not use a real database.
 * This is another LOW-LEVEL DETAIL used for testing.
 */
public class MockGreetingRepository implements GreetingRepository {
    @Override
    public void saveName(String name) throws SQLException {
        // No database connection! Just pretend it worked and print to console.
        if (name.equals("fail")) {
            throw new SQLException("Simulated database failure.");
        }
        System.out.println("MockGreetingRepository: Successfully 'saved' name -> " + name);
    }
}
```

**Step 3: Refactor the GUI to Depend on the Abstraction**
Finally, we modify our main `GreeterApp` class. The `ActionListener` (Controller) will now hold a reference to the `GreetingRepository` interface. The specific implementation (real or mock) will be "injected" into it.

```java
// File: GreeterApp.java (Refactored)
import javax.swing.*;
import java.awt.*;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;
import java.sql.SQLException;

public class GreeterApp extends JFrame {
    // The Controller (ActionListener) now depends on the INTERFACE, not a concrete class.
    private final GreetingRepository repository;
    
    private JTextField nameField;
    private JLabel resultLabel;

    public GreeterApp(GreetingRepository repository) {
        this.repository = repository; // The dependency is "injected" here.
        
        // --- GUI Setup ---
        setTitle("Greeter App");
        setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        setSize(400, 200);
        setLayout(new FlowLayout(FlowLayout.CENTER, 10, 20));

        nameField = new JTextField(15);
        JButton greetButton = new JButton("Greet");
        JButton clearButton = new JButton("Clear");
        JButton saveButton = new JButton("Save to DB");
        resultLabel = new JLabel("Enter your name and click a button.");

        add(new JLabel("Name:"));
        add(nameField);
        add(greetButton);
        add(clearButton);
        add(saveButton);
        add(resultLabel);
        
        // --- Event Handling ---
        greetButton.addActionListener(e -> greetUser());
        clearButton.addActionListener(e -> clearFields());
        saveButton.addActionListener(e -> saveUser());
    }

    private void greetUser() {
        String name = nameField.getText();
        resultLabel.setText(name.isEmpty() ? "Please enter a name!" : "Hello, " + name + "!");
    }

    private void clearFields() {
        nameField.setText("");
        resultLabel.setText("Enter your name and click a button.");
    }
    
    // This is our Controller's logic
    private void saveUser() {
        String name = nameField.getText();
        if (name.isEmpty()) {
            JOptionPane.showMessageDialog(this, "Name cannot be empty.", "Error", JOptionPane.ERROR_MESSAGE);
            return;
        }

        try {
            // The Controller calls the interface method, unaware of the implementation.
            repository.saveName(name);
            JOptionPane.showMessageDialog(this, "Name '" + name + "' saved successfully!");
        } catch (SQLException ex) {
            JOptionPane.showMessageDialog(this, "Database error: " + ex.getMessage(), "Error", JOptionPane.ERROR_MESSAGE);
        }
    }

    public static void main(String[] args) {
        // --- To run the REAL application, we inject the REAL database repository ---
        GreetingRepository realRepository = new JdbcGreetingRepository();
        
        SwingUtilities.invokeLater(() -> {
            GreeterApp app = new GreeterApp(realRepository);
            app.setVisible(true);
        });
    }
}
```

#### **3. How This Enables Unit-Testing**

With the Dependency Inversion Principle applied, our Controller (the logic within the `saveUser` method and its listeners) is now completely decoupled from the real database. We can now write a simple unit test for it without needing a database connection.

A unit test (using a framework like JUnit) would look like this:

```java
// This is a conceptual unit test, not part of the main application.
class GreeterAppTest {
    
    // A test method.
    public void testSaveUser_Success() {
        // 1. Setup: Create a MOCK repository, not a real one.
        GreetingRepository mockRepo = new MockGreetingRepository();
        
        // 2. Create the GUI, injecting the MOCK dependency.
        GreeterApp testApp = new GreeterApp(mockRepo);
        
        // 3. Action: Simulate user input and button click.
        testApp.nameField.setText("TestUser");
        testApp.saveButton.doClick();
        
        // 4. Assert: Check if the outcome was as expected.
        // In a real test, we would check if a success dialog was shown.
        // For this example, we rely on the console output from the mock object:
        // "MockGreetingRepository: Successfully 'saved' name -> TestUser"
        // This proves the controller logic works without ever touching a database.
    }
}
```

By applying DIP, we have made our high-level controller logic independent of low-level data access details, making it robust, flexible, and, most importantly, **testable in isolation**.
