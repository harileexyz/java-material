Excellent choice. A login flow is a far more realistic and engaging project. It naturally lends itself to separating concerns into different classes and provides a perfect opportunity to teach the Model-View-Controller (MVC) pattern in a clear, practical way.

Here is a complete, extensive teaching guide to build a simple Login application, structured around the MVC pattern.

---
---

## **Live Project-Based Teaching Guide: Building a Login Application with MVC in Java Swing**

**Objective:** To teach all fundamental Swing and Event Handling concepts by building a multi-screen login application. This project will be structured using the Model-View-Controller (MVC) design pattern to promote good software design habits.

**The Project:** A simple login application.
1.  A **Login Screen** will accept a username and password.
2.  A **"Login" button** will validate the credentials against hardcoded values.
3.  If successful, the login screen will close, and a **Home Screen** will open, displaying a welcome message.
4.  If unsuccessful, an error message will be shown.

---

### **Part 1: Understanding the MVC Pattern for Our Login App**

#### **Teaching Script - Introduction**

"Today, we're building a complete, multi-screen login application. More importantly, we're going to build it the *right way*, using a famous design pattern called **Model-View-Controller**, or **MVC**. This pattern is used everywhere in software development, from desktop apps to web applications, because it keeps our code organized, clean, and easy to manage."

"MVC separates our application into three distinct parts:"

1.  **Model:** The **BRAINS** of the application. It holds the data and the business logic. It knows nothing about what the app looks like.
    *   **In our project:** The `UserModel` will hold the correct username/password and the logic to check if the input is valid.

2.  **View:** The **FACE** of the application. It's the user interface (UI) that the user sees and interacts with. It's responsible for displaying data from the Model but doesn't contain any business logic.
    *   **In our project:** The `LoginView` (our login window) and `HomeView` (our welcome window).

3.  **Controller:** The **MIDDLEMAN** or the **TRAFFIC COP**. It listens for user input from the View, tells the Model to do its work, and then tells the View to update its display.
    *   **In our project:** The `LoginController` will listen for the button click, get the text from the `LoginView`, ask the `UserModel` to validate it, and then decide whether to show an error or open the `HomeView`.

#### **MVC Diagram for Our Project**

"Here’s how these three parts will communicate in our login app:"



(You can draw this on a whiteboard or show this image).

1.  **User interacts with `LoginView`** (types username/password, clicks "Login").
2.  The **`LoginView` notifies the `LoginController`** about the button click.
3.  The **`LoginController` gets the input data** (username/password) from the `LoginView`.
4.  The **`LoginController` asks the `UserModel`** to `validateCredentials()`.
5.  The **`UserModel` performs the business logic** (compares the input to the correct credentials) and returns `true` or `false`.
6.  The **`LoginController` receives the result** from the Model.
7.  Based on the result, the **`LoginController` tells the `LoginView`** to either show an error message OR it creates and shows the `HomeView`.

---

### **Part 2: Building the Project Step-by-Step in IntelliJ**

#### **Step 1: Setting up the Project Structure (Packages)**

1.  In IntelliJ, create a new Java project named `LoginApp`.
2.  In the `src` folder, create three packages to represent our MVC structure:
    *   `com.app.model`
    *   `com.app.view`
    *   `com.app.controller`

Your project structure should look like this:
```
LoginApp/
└── src/
    └── com/
        └── app/
            ├── controller/
            ├── model/
            └── view/
```

#### **Step 2: Creating the Model**

"Let's start with the simplest part: the brains. The Model doesn't care about windows or buttons."

1.  Right-click `com.app.model` → **New** → **Java Class** → name it `UserModel`.
2.  Add this code:

```java
// File: src/com/app/model/UserModel.java
package com.app.model;

// The MODEL: Holds data and business logic.
public class UserModel {
    // Hardcoded correct credentials (in a real app, this would come from a database).
    private static final String CORRECT_USERNAME = "btech";
    private static final String CORRECT_PASSWORD = "java";

    // Business Logic: The single responsibility of this model is to validate credentials.
    public boolean validateCredentials(String username, String password) {
        // Simple comparison logic.
        return CORRECT_USERNAME.equals(username) && CORRECT_PASSWORD.equals(password);
    }
}
```
**Teaching Point:** "Notice this class is pure Java. No Swing code. It has one job: validation. This is the Single Responsibility Principle in action."

#### **Step 3: Creating the Views**

"Next, let's build the user interfaces. The Views are 'dumb'—they only know how to display components and report user actions."

1.  Right-click `com.app.view` → **New** → **Java Class** → name it `LoginView`.
2.  Add this code for our login window:

```java
// File: src/com/app/view/LoginView.java
package com.app.view;

import javax.swing.*;
import java.awt.event.ActionListener;

// The VIEW: Only responsible for the UI. It's a 'dumb' screen.
public class LoginView extends JFrame {
    private JTextField usernameField;
    private JPasswordField passwordField; // Use JPasswordField for passwords
    private JButton loginButton;

    public LoginView() {
        setTitle("Login");
        setSize(350, 200);
        setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        setLocationRelativeTo(null); // Center the window

        JPanel panel = new JPanel();
        panel.setLayout(new BoxLayout(panel, BoxLayout.Y_AXIS));

        panel.add(new JLabel("Username:"));
        usernameField = new JTextField(15);
        panel.add(usernameField);

        panel.add(new JLabel("Password:"));
        passwordField = new JPasswordField(15);
        panel.add(passwordField);

        loginButton = new JButton("Login");
        panel.add(loginButton);
        
        add(panel);
    }
    
    // --- Methods for the Controller to interact with the View ---
    
    public String getUsername() {
        return usernameField.getText();
    }

    public String getPassword() {
        // JPasswordField returns a char array for security, we convert it to a String.
        return new String(passwordField.getPassword());
    }

    public void addLoginListener(ActionListener listener) {
        loginButton.addActionListener(listener);
    }

    public void displayErrorMessage(String message) {
        JOptionPane.showMessageDialog(this, message, "Login Error", JOptionPane.ERROR_MESSAGE);
    }
}
```
**Teaching Point:** "Look at the methods at the bottom. The View provides simple ways for the Controller to `get` data from it (`getUsername`) and `add` a listener. It doesn't know *what* will happen when the button is clicked; it just reports that it *was* clicked."

3.  Right-click `com.app.view` → **New** → **Java Class** → name it `HomeView`.
4.  Add this code for our welcome screen:

```java
// File: src/com/app/view/HomeView.java
package com.app.view;

import javax.swing.*;
import java.awt.*;

// The second VIEW: A simple welcome screen.
public class HomeView extends JFrame {
    public HomeView(String username) {
        setTitle("Home Page");
        setSize(400, 300);
        setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        setLocationRelativeTo(null);

        JLabel welcomeLabel = new JLabel("Welcome, " + username + "!", SwingConstants.CENTER);
        welcomeLabel.setFont(new Font("Serif", Font.BOLD, 24));
        
        add(welcomeLabel);
    }
}
```

#### **Step 4: Creating the Controller**

"Now for the most important part: the Controller. It will connect our Model and View."

1.  Right-click `com.app.controller` → **New** → **Java Class** → name it `LoginController`.
2.  Add this code:

```java
// File: src/com/app/controller/LoginController.java
package com.app.controller;

import com.app.model.UserModel;
import com.app.view.HomeView;
import com.app.view.LoginView;

import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;

// The CONTROLLER: The middleman that connects the Model and View.
public class LoginController {
    private UserModel model;
    private LoginView view;

    public LoginController(UserModel model, LoginView view) {
        this.model = model;
        this.view = view;
        
        // Add the listener to the view.
        // The 'this::handleLogin' is a method reference, a modern way to write the listener.
        // You can also write 'new LoginListener()' and create an inner class.
        this.view.addLoginListener(e -> handleLogin());
    }
    
    private void handleLogin() {
        // 1. Get user input from the View
        String username = view.getUsername();
        String password = view.getPassword();
        
        // 2. Ask the Model to validate the credentials
        if (model.validateCredentials(username, password)) {
            // 3a. If successful, close the login view and open the home view
            System.out.println("Login Successful!");
            view.dispose(); // Close the login window
            HomeView homeView = new HomeView(username);
            homeView.setVisible(true);
        } else {
            // 3b. If unsuccessful, tell the View to display an error message
            System.out.println("Login Failed!");
            view.displayErrorMessage("Invalid username or password.");
        }
    }
}
```

#### **Step 5: The `Main` Class (The Application Starter)**

"Finally, we need a starting point for our application. This `Main` class will create our M, V, and C objects and link them together."

1.  Create a new package `com.app`.
2.  Right-click `com.app` → **New** → **Java Class** → name it `Main`.
3.  Add this code:

```java
// File: src/com/app/Main.java
package com.app;

import com.app.controller.LoginController;
import com.app.model.UserModel;
import com.app.view.LoginView;

import javax.swing.*;

public class Main {
    public static void main(String[] args) {
        // Use SwingUtilities.invokeLater to ensure the GUI is created on the Event Dispatch Thread (EDT)
        // This is a best practice for all Swing applications.
        SwingUtilities.invokeLater(new Runnable() {
            @Override
            public void run() {
                // 1. Create the Model
                UserModel model = new UserModel();
                
                // 2. Create the View
                LoginView view = new LoginView();
                
                // 3. Create the Controller and link the Model and View
                new LoginController(model, view);
                
                // 4. Make the initial view visible
                view.setVisible(true);
            }
        });
    }
}
```
**To Run:** Right-click the `Main.java` file and select **Run 'Main.main()'**.

### **Live Class Walkthrough**
1.  Run the application. The login window appears.
2.  **Try incorrect credentials:** Enter `admin` / `password` and click "Login". An error message dialog pops up. Explain that the Controller asked the Model, the Model said `false`, so the Controller told the View to show the error.
3.  **Try correct credentials:** Enter `btech` / `java` and click "Login". The login window closes, and the Home window appears with "Welcome, btech!". Explain that this time the Model said `true`, so the Controller closed the old View and created the new `HomeView`.

This project successfully covers all the required topics in a structured, professional, and highly practical way.
