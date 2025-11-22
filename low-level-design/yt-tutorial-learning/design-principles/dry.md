# DRY

## DRY Principle

> **Source:** [Original Article](https://codewitharyan.com/tech-blogs/dry-principle)

### Overview

In the world of software development, clean and maintainable code is the foundation of scalable and robust applications. One of the core principles that guides developers in achieving this is the **DRY Principle**.

DRY stands for **Don't Repeat Yourself**, and adhering to this principle can significantly improve code quality and reduce redundancy.

#### What is DRY?

**Don't Repeat Yourself (DRY)** is a software development principle that encourages developers to avoid duplicating code in a system. The main idea behind DRY is to reduce redundancy and promote efficiency by ensuring that a particular piece of knowledge or logic exists in only one place within a codebase.

When developers adhere to the DRY principle, they aim to create reusable components, functions, or modules that can be utilized in various parts of the codebase. This not only makes the code more maintainable but also minimizes the chances of errors since changes or updates only need to be made in one location.

***

### Key Features of The DRY Principle

The key features of the Don't Repeat Yourself (DRY) principle in software development include:

#### 1. Code Reusability

DRY encourages developers to write code in a way that minimizes redundancy. Instead of duplicating code, developers should create reusable components, functions, or modules that can be shared and applied in multiple parts of the codebase.

#### 2. Maintenance and Updates

By adhering to DRY, developers reduce the likelihood of errors and bugs that can arise from inconsistent updates. Since a particular piece of logic or knowledge exists in only one place, any changes or enhancements can be made in a centralized location, making maintenance more efficient.

#### 3. Readability

DRY contributes to code readability by eliminating unnecessary repetition. When developers follow the principle, it becomes easier for others (or even themselves) to understand and navigate the codebase since there are fewer instances of similar or identical code scattered throughout.

#### 4. Consistency

DRY promotes consistency in the codebase. When a specific functionality is encapsulated in a single location, it ensures that all instances of that functionality behave consistently. This is crucial for creating reliable and predictable software.

#### 5. Reduced Development Time

By reusing code instead of rewriting it, developers can significantly reduce the time and effort required for development. This is particularly valuable when building large and complex software systems, as it streamlines the development process.

#### 6. Facilitates Collaboration

DRY enhances collaboration among team members. When code is modular and reusable, it becomes easier for multiple developers to work on different parts of the system without interfering with each other. Each developer can focus on a specific component or module without duplicating efforts.

#### 7. Avoidance of Copy-Paste Errors

Copying and pasting code can introduce errors, especially if changes are made inconsistently across duplicated sections. DRY minimizes the need for copy-pasting by encouraging the creation of reusable units of code, reducing the risk of introducing errors.

#### 8. Testability

Reusable and modular code is often easier to test since specific functionalities are encapsulated in distinct units. This makes it simpler to write unit tests and ensure that changes do not inadvertently affect unrelated parts of the system.

***

### How to Implement the DRY Principle

#### 1. Use Functions or Methods

Encapsulate repetitive code into reusable functions or methods.

**Example:**

```java
public class NumberSwapper {
    // Non-DRY approach - repeating swap logic multiple places
    public void processNumbersNonDry() {
        int a = 5;
        int b = 10;
        
        // Swapping values here
        int temp = a;
        a = b;
        b = temp;
        
        // Later in the code, need to swap different numbers
        int x = 20;
        int y = 30;
        
        // Repeating the same swap logic
        temp = x;
        x = y;
        y = temp;
    }

    // DRY approach - creating a reusable swap method
    public void swap(int[] numbers) {
        if (numbers.length >= 2) {
            int temp = numbers[0];
            numbers[0] = numbers[1];
            numbers[1] = temp;
        }
    }

    // Example usage
    public static void main(String[] args) {
        NumberSwapper swapper = new NumberSwapper();
        int[] numbers = {5, 10};
        
        System.out.println("Before swap: " + numbers[0] + ", " + numbers[1]);
        swapper.swap(numbers);
        System.out.println("After swap: " + numbers[0] + ", " + numbers[1]);
    }
}
```

**Output:**

```
Before swap: 5, 10
After swap: 10, 5
```

> **Key Point:** By creating a reusable `swap()` method, we eliminate code duplication and make the logic easier to maintain. Any changes to the swap logic only need to be made in one place.

***

#### 2. Leverage Object-Oriented Principles

Use inheritance, polymorphism, and interfaces to share behavior between classes.

**DRY Violation Code**

```java
// SubmitButton class with its own onClick() implementation
class SubmitButton {
    void onClick() {
        System.out.println("Form submitted.");
    }
}

// CancelButton class with its own onClick() implementation
class CancelButton {
    void onClick() {
        System.out.println("Action canceled.");
    }
}

public class Main {
    public static void main(String[] args) {
        SubmitButton submit = new SubmitButton();
        submit.onClick();  // Output: Form submitted.
        
        CancelButton cancel = new CancelButton();
        cancel.onClick();  // Output: Action canceled.
    }
}
```

**Output:**

```
Form submitted.
Action canceled.
```

**Why This Violates DRY:**

In this implementation, we have separate classes (`SubmitButton` and `CancelButton`), each with its own `onClick()` method.

In this approach, if you introduce new buttons, you would need to repeat the `onClick()` implementation each time. This is a violation of the DRY principle, as the code would need to duplicate logic for every new button type. If the button logic were more complex, this could lead to increased maintenance, inconsistencies, and errors, as every time we add a new button, we must remember to write the same `onClick()` logic.

***

**Adhering To DRY Code**

```java
// Base class
abstract class Button {
    abstract void onClick();
}

// Subclass implementing specific behavior
class SubmitButton extends Button {
    @Override
    void onClick() {
        System.out.println("Form submitted.");
    }
}

// Subclass implementing different behavior
class CancelButton extends Button {
    @Override
    void onClick() {
        System.out.println("Action canceled.");
    }
}

public class Main {
    public static void main(String[] args) {
        Button submit = new SubmitButton();
        submit.onClick();  // Output: Form submitted.
        
        Button cancel = new CancelButton();
        cancel.onClick();  // Output: Action canceled.
    }
}
```

**Output:**

```
Form submitted.
Action canceled.
```

**Benefits:**

In this approach, if you introduce new buttons, you do not need to repeat the `onClick()` implementation each time. The code would simply need to override the `onClick()` method of the abstract class and implement its own logic for each new button type. This ensures that the common behavior is defined in the abstract class, while the specific behavior for each button type is implemented in the subclasses.

***

#### 3. Create Reusable Components

In Java, reusable components are often created as methods, classes, or utility libraries to avoid duplicating similar logic or UI code.

**Example:**

```java
// Reusable method for button rendering
public class Button {
    private String label;
    
    public Button(String label) {
        this.label = label;
    }
    
    public void render() {
        System.out.println("Rendering button: " + label);
    }
}

public class Main {
    public static void main(String[] args) {
        Button submitButton = new Button("Submit");
        submitButton.render();  // Output: Rendering button: Submit
        
        Button cancelButton = new Button("Cancel");
        cancelButton.render();  // Output: Rendering button: Cancel
    }
}
```

**Output:**

```
Rendering button: Submit
Rendering button: Cancel
```

> **Key Point:** By creating a reusable `Button` class, we can create multiple buttons with different labels without duplicating the rendering logic.

***

#### 4. Use Constants and Configuration Files

Avoid hardcoding values by defining them in a single location.

**Example:**

**Before DRY**

```java
public class Main {
    public static void main(String[] args) {
        System.out.println("Connecting to http://example.com");
    }
}
```

**After DRY**

```java
// Constants class
public class Config {
    public static final String BASE_URL = "http://example.com";
}

// Main class
public class Main {
    public static void main(String[] args) {
        System.out.println("Connecting to " + Config.BASE_URL);
        // Output: Connecting to http://example.com
    }
}
```

**Output:**

```
Connecting to http://example.com
```

**Benefits:**

* If the URL needs to change, we only update it in one place (`Config.BASE_URL`)
* All references to the URL automatically use the updated value
* Reduces the risk of inconsistencies and typos

***

### Advantages and Disadvantages of DRY

#### Advantages

| Advantage           | Description                                                                                             |
| ------------------- | ------------------------------------------------------------------------------------------------------- |
| **Efficiency**      | Reduces the amount of code written, saving development time                                             |
| **Maintainability** | Changes in logic or functionality only need to be applied once, reducing the risk of introducing errors |
| **Scalability**     | Modular and reusable code makes it easier to extend the application                                     |
| **Consistency**     | Ensures uniform behavior across the application                                                         |
| **Collaboration**   | Clean, organized code improves teamwork and reduces onboarding time for new developers                  |

***

#### Disadvantages

| Disadvantage                | Description                                                                                                  |
| --------------------------- | ------------------------------------------------------------------------------------------------------------ |
| **Over-Abstraction Risks**  | Too much abstraction can make code harder to read and debug                                                  |
| **Initial Time Investment** | Writing reusable code often requires more upfront planning and effort                                        |
| **Misuse**                  | Applying DRY inappropriately to unrelated functionalities can lead to tight coupling and reduced flexibility |
| **Complex Refactoring**     | Refactoring legacy code to adhere to DRY can be time-consuming and error-prone                               |

***

### When NOT to Apply DRY

While DRY is a powerful principle, there are scenarios where code duplication might be acceptable or even preferable:

#### 1. Different Contexts

If two pieces of code look similar but serve different purposes or are likely to evolve independently, keeping them separate might be better.

**Example:**

```java
// User validation in authentication
boolean validateUser(String username) {
    return username != null && username.length() >= 3;
}

// Product name validation in inventory
boolean validateProductName(String name) {
    return name != null && name.length() >= 3;
}
```

Even though the logic looks similar, these validations serve different domains and may evolve differently (e.g., user validation might require special characters, while product names might not).

#### 2. Performance Critical Code

Sometimes, abstraction can introduce performance overhead. In performance-critical sections, some duplication might be acceptable.

#### 3. Early Development

During prototyping or proof-of-concept development, it's okay to duplicate code temporarily. DRY can be applied during refactoring once the design stabilizes.

***

### Best Practices for Applying DRY

1. **Identify true duplication:** Not all similar-looking code is duplication. Ensure the logic truly represents the same concept.
2. **Extract common logic gradually:** Don't try to eliminate all duplication at once. Refactor incrementally.
3. **Use meaningful abstractions:** When creating reusable components, ensure they have clear, single purposes.
4. **Balance DRY with other principles:** Consider SOLID principles, KISS (Keep It Simple, Stupid), and YAGNI (You Aren't Gonna Need It).
5. **Document reusable components:** Make it easy for other developers to discover and use shared code.
6. **Avoid premature abstraction:** Wait until you have at least three instances of duplication before abstracting (Rule of Three).
7. **Test thoroughly:** When refactoring to eliminate duplication, ensure comprehensive test coverage.
8. **Consider the cost:** Sometimes a small amount of duplication is better than a complex abstraction.

***

### DRY in Different Scenarios

#### Database Queries

**Before DRY:**

```java
public User getUserById(int id) {
    // Connection and query logic repeated
    Connection conn = DriverManager.getConnection(url, user, password);
    Statement stmt = conn.createStatement();
    ResultSet rs = stmt.executeQuery("SELECT * FROM users WHERE id = " + id);
    // Process result...
}

public User getUserByEmail(String email) {
    // Same connection logic repeated
    Connection conn = DriverManager.getConnection(url, user, password);
    Statement stmt = conn.createStatement();
    ResultSet rs = stmt.executeQuery("SELECT * FROM users WHERE email = '" + email + "'");
    // Process result...
}
```

**After DRY:**

```java
public class DatabaseHelper {
    private static Connection getConnection() {
        return DriverManager.getConnection(url, user, password);
    }
    
    public static ResultSet executeQuery(String query) {
        Connection conn = getConnection();
        Statement stmt = conn.createStatement();
        return stmt.executeQuery(query);
    }
}

public User getUserById(int id) {
    ResultSet rs = DatabaseHelper.executeQuery("SELECT * FROM users WHERE id = " + id);
    // Process result...
}

public User getUserByEmail(String email) {
    ResultSet rs = DatabaseHelper.executeQuery("SELECT * FROM users WHERE email = '" + email + "'");
    // Process result...
}
```

***

### Summary

The Don't Repeat Yourself (DRY) principle is a fundamental guideline in software development that promotes code efficiency, readability, and maintainability.

#### Key Takeaways

**Core Concept:**

* Avoid duplicating code by creating reusable components, functions, and modules
* Ensure each piece of knowledge or logic exists in only one place

**Implementation Strategies:**

1. Use functions or methods to encapsulate repetitive logic
2. Leverage object-oriented principles (inheritance, polymorphism, interfaces)
3. Create reusable components and utility classes
4. Use constants and configuration files for shared values

**Benefits:**

* Reduced development time through code reuse
* Easier maintenance with centralized updates
* Improved consistency across the application
* Better collaboration among team members
* Reduced risk of copy-paste errors

**Considerations:**

* Avoid over-abstraction that makes code harder to understand
* Balance DRY with other principles (SOLID, KISS, YAGNI)
* Apply the Rule of Three before abstracting
* Consider performance implications in critical sections

***

### Conclusion

In conclusion, the Don't Repeat Yourself (DRY) approach promotes readability, maintainability, and code efficiency and is a fundamental guideline in software development. DRY lowers the chance of errors, improves collaboration, and facilitates maintenance by encouraging code reuse and decreasing redundancy.

The advantages of DRY must be weighed against any potential drawbacks, such as dependency problems, over-abstraction, and premature optimization. In the end, using DRY in conjunction with other complementary concepts encourages the development of reliable, scalable, and maintainable software systems.

Developers are contributing to a culture of excellence and efficiency in software engineering as they continue to perfect their processes and embrace DRY. By understanding when and how to apply the DRY principle effectively, developers can create code that is not only functional but also elegant, maintainable, and scalable.

***

### Next Steps

Continue your learning journey by exploring:

* SOLID principles and how they complement DRY
* Refactoring techniques for eliminating code duplication
* Design patterns that promote code reuse
* Code review practices for identifying duplication
* Static analysis tools for detecting code duplication
