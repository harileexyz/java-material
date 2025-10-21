

## **Quick Revision Guide: Swing & Event Handling with Code Examples**

This guide provides short, precise definitions, analogies, and minimal code examples for key Swing and Event Handling concepts, tailored for answering short exam questions.

### **Part 1: Core Swing Concepts**

#### **1. Components and Containers**
*   **Component:** The fundamental visual building block.
    *   **Analogy:** A **picture** on a wall.
    *   **Code Example:** `JButton myButton = new JButton("Click Me");`

*   **Container:** A special component that holds and organizes other components.
    *   **Analogy:** A **picture frame (`JPanel`)** or the **wall (`JFrame`)**.
    *   **Code Example:**
        ```java
        JPanel panel = new JPanel(); // A container
        JButton button = new JButton("OK"); // A component
        panel.add(button); // Placing the component inside the container
        ```

#### **2. Swing Controls (Core Components)**
*   **`JFrame`:** The main application window.
    *   **Analogy:** The **house** which contains all the rooms.
    *   **Code Example:**
        ```java
        JFrame frame = new JFrame("My Application");
        frame.setSize(400, 300);
        frame.setVisible(true);
        ```

*   **`JLabel`:** Displays non-editable text or an image.
    *   **Analogy:** A **label on a jar**.
    *   **Code Example:** `JLabel nameLabel = new JLabel("Enter your name:");`

*   **`JButton`:** A button that triggers an action.
    *   **Analogy:** A **doorbell button**.
    *   **Code Example:** `JButton submitButton = new JButton("Submit");`

*   **`JTextField`:** A single-line text input box.
    *   **Analogy:** A **blank line on a form**.
    *   **Code Example:** `JTextField nameField = new JTextField(20); // 20 is the approximate width`

#### **3. Swing Packages**
*   **Definition:** Namespaces for grouping related classes. You use `import` to access them.
*   **Code Example:**
    ```java
    import javax.swing.*;      // For JFrame, JButton, etc.
    import java.awt.*;         // For Layout Managers like GridLayout.
    import java.awt.event.*; // For ActionListener and other event classes.
    ```

#### **4. Swing Layout Managers**
*   **Definition:** An object that controls the size and position of components in a container.
*   **Analogy:** An **interior designer** for your window.
*   **Code Example (`GridLayout`):**
    ```java
    JPanel panel = new JPanel();
    // Set the layout to a 2x2 grid.
    panel.setLayout(new GridLayout(2, 2)); 
    
    panel.add(new JLabel("Name:"));
    panel.add(new JTextField());
    panel.add(new JLabel("Email:"));
    panel.add(new JTextField());
    ```

#### **5. Model-View-Controller (MVC)**
*   **Definition:** A design pattern that separates application logic into three parts:
    *   **Model:** The data and business logic (The Kitchen).
    *   **View:** The UI that the user sees (The Menu & Dining Area).
    *   **Controller:** Handles user input and connects the Model and View (The Waiter).
*   **Code Example (Conceptual):**
    ```java
    // Model: Holds the data
    class UserModel { String name; }

    // View: Displays the data
    class UserView { JTextField nameField; }

    // Controller: Connects them
    class UserController {
        UserModel model;
        UserView view;
        void updateModelFromView() {
            model.name = view.nameField.getText();
        }
    }
    ```

---

### **Part 2: Event Handling Concepts**

#### **6. The Delegation Event Model**
*   **Definition:** Java's event handling system where a component (Source) delegates the task of handling an event to a separate object (Listener).
*   **The Three Parts:**
    1.  **Event Source:** The component that originates the event (e.g., a `JButton`).
    2.  **Event Object:** An object created to describe the event (e.g., `ActionEvent`).
    3.  **Event Listener:** An object that receives and handles the event (e.g., `ActionListener`).

#### **7. Event Sources**
*   **Definition:** The GUI component that generates an event.
*   **Analogy:** The **doorbell button**.
*   **Code Example:** In `myButton.addActionListener(...)`, `myButton` is the **Event Source**.

#### **8. Event Classes (and Event Objects)**
*   **Definition:** An object containing information about the event that occurred.
*   **Analogy:** The **phone call to order a pizza**, containing the order details.
*   **Code Example:**
    ```java
    public void actionPerformed(ActionEvent e) {
        // 'e' is the Event Object. We can inspect it.
        Object source = e.getSource(); // Which button was clicked?
        System.out.println("An action occurred!");
    }
    ```

#### **9. Event Listener Interfaces**
*   **Definition:** An interface that a class must implement to handle a specific type of event. It defines the "contract" for what methods the handler must have.
*   **Analogy:** The **pizza shop employee's job description**, which says they must know how to `takeOrder()`.
*   **Code Example (`ActionListener`):**
    ```java
    // A class that PROMISES to handle ActionEvents
    class MyButtonListener implements ActionListener {
        // It MUST provide this method.
        @Override
        public void actionPerformed(ActionEvent e) {
            System.out.println("Button was clicked!");
        }
    }
    ```

#### **10. Using the Delegation Event Model (Putting it all together)**

This is the complete three-step process.

**Step-by-Step Code Example:**
```java
import javax.swing.*;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;

public class EventHandlingDemo {
    public static void main(String[] args) {
        JFrame frame = new JFrame("Event Demo");
        JButton button = new JButton("Click Me"); // This is the Event Source

        // --- Step 1 & 2: Create a Listener object and implement its methods ---
        // We are using an "anonymous inner class" here for simplicity.
        ActionListener listener = new ActionListener() {
            // This is the method that will run when the event occurs.
            @Override
            public void actionPerformed(ActionEvent e) { 
                // 'e' is the Event Object.
                JOptionPane.showMessageDialog(null, "Button was clicked!");
            }
        };

        // --- Step 3: Register the listener with the source ---
        // We are "delegating" the handling of clicks on 'button' to our 'listener'.
        button.addActionListener(listener);

        // Standard frame setup
        frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        frame.add(button);
        frame.pack();
        frame.setVisible(true);
    }
}
```
