# Behavioural Design Pattern Introduction

## Behavioral Design Pattern Introduction

> **Source:** [Original Article](https://codewitharyan.com/tech-blogs/behavioral-design-pattern)

### Behavioral Design Patterns: Enhancing Communication Between Objects

In the world of Object-Oriented Programming (OOP), we deal with various challenges related to how objects interact with one another. One of the key areas is the **communication between objects**.

#### Real-World Analogy

Imagine you have a bunch of friends who want to go to a party. But instead of calling each one individually, you all use a **group chat** to send messages to everyone at once. This saves time and makes the communication easier!

In the world of software, this concept of efficient communication between objects is achieved through **Behavioral Design Patterns**. But why are they called "behavioral" patterns?

***

### What Are Behavioral Design Patterns?

Behavioral design patterns are all about **how objects interact and communicate** with each other. These patterns focus on the behavior of objects, how they collaborate to complete a task, and how the flow of control is managed between them.

**In simple terms:** They help in defining the roles and responsibilities of objects in a way that makes communication clear and organized.

You can think of it as giving your objects a better way to communicate without being chaotic. Just like how you'd communicate with friends using a structured group chat, objects use these patterns to talk to each other efficiently, without causing confusion or unnecessary mess.

***

### Why Are They Called Behavioral Patterns?

The term **"behavioral"** comes from the fact that these patterns define the **behavior of objects in relation to one another**. They don't focus on the objects themselves (which would be like looking at a person's traits), but rather on the **interactions between them**.

**Key Point:** It's not about what the object **is** (like its properties), but rather what it **does** when it communicates with other objects.

#### Focus Areas

| Aspect      | Structural Patterns              | Behavioral Patterns                  |
| ----------- | -------------------------------- | ------------------------------------ |
| **Focus**   | Object composition and structure | Object interaction and communication |
| **Concern** | How objects are built            | How objects behave and collaborate   |
| **Example** | Class hierarchy, interfaces      | Message passing, responsibilities    |

***

### Why Are Behavioral Design Patterns Useful?

#### 1. Clearer Communication

These patterns make it easier for objects to communicate in a structured and organized way. This is especially important in large and complex systems, where keeping the communication lines clean can prevent bugs and confusion.

**Benefit:** Reduces complexity in object interactions

***

#### 2. Decoupling Objects

One of the coolest things about behavioral patterns is that they help to **decouple objects**. This means the objects don't need to know each other too well, which makes it easier to modify one object without affecting the rest.

**Analogy:** It's like making new friends who don't need to know your entire life story to have a good chat!

**Benefit:** Loose coupling leads to more maintainable code

***

#### 3. Flexibility

These patterns often make your code more flexible by allowing you to change or extend how objects behave without modifying their classes.

**Analogy:** It's like being able to change your mind about what type of message to send in that group chat, but without messing up the entire conversation.

**Benefit:** Easy to extend and modify behavior

***

#### 4. Better Organization

Behavioral patterns provide a clear structure for object communication, making the system easier to understand and manage, especially as your codebase grows.

**Benefit:** Improved code readability and maintainability

***

### Key Benefits Summary

| Benefit                   | Description                                     | Impact                        |
| ------------------------- | ----------------------------------------------- | ----------------------------- |
| **Clearer Communication** | Structured interactions between objects         | Fewer bugs, less confusion    |
| **Decoupling**            | Objects don't need deep knowledge of each other | Easier to modify and maintain |
| **Flexibility**           | Change behavior without changing classes        | Adaptable to new requirements |
| **Better Organization**   | Clear structure for interactions                | Scalable codebase             |

***

### Popular Behavioral Design Patterns

There are many well-known behavioral design patterns, each addressing specific communication or control flow needs. Here are the most common ones:

#### 1. Observer Pattern

**Concept:** Think of it as a newsfeed on social media. When something important happens (like a new post), all the people (observers) following it get updated automatically! No need to check in every time.

**Use Case:**

* Event handling systems
* News feeds
* Stock price updates
* GUI event listeners

**How It Works:**

* Subjects maintain a list of observers
* When state changes, all observers are notified
* One-to-many dependency between objects

**Example Scenario:**

```
Subject (NewsAgency) → publishes news
Observers (Users, Websites, Apps) → receive updates automatically
```

***

#### 2. Strategy Pattern

**Concept:** It's like having a set of game plans for different situations. For example, if you're playing soccer, your team could use different strategies depending on whether you're attacking or defending.

**Use Case:**

* Payment processing (credit card, PayPal, cryptocurrency)
* Sorting algorithms (quick sort, merge sort, bubble sort)
* Compression algorithms
* Navigation routes

**How It Works:**

* Define a family of algorithms
* Encapsulate each one
* Make them interchangeable
* Strategy pattern lets you switch between behaviors (strategies) without changing the object's class

**Example Scenario:**

```
Context (PaymentProcessor)
Strategies (CreditCardPayment, PayPalPayment, CryptoPayment)
```

***

#### 3. Command Pattern

**Concept:** This one's like the remote control for your TV. You can press different buttons to make the TV do different things, but each button press is treated as a separate command.

**Use Case:**

* GUI buttons and menu items
* Macro recording
* Transaction systems
* Undo/redo functionality

**How It Works:**

* Encapsulates a request as an object
* Lets you execute, undo, or queue up commands
* Decouples sender from receiver

**Example Scenario:**

```
Remote Control (Invoker)
Commands (TurnOnCommand, TurnOffCommand, ChangeChannelCommand)
TV (Receiver)
```

***

#### 4. Chain of Responsibility Pattern

**Concept:** Imagine you have a series of help desks for tech support. If the first person can't solve the problem, they send it to the next one.

**Use Case:**

* Exception handling
* Authentication chains
* Logging frameworks
* Event bubbling in UI

**How It Works:**

* Passes request along a chain of handlers
* Each handler has a chance to process it or pass it on
* Decouples sender from receiver

**Example Scenario:**

```
Request → Level 1 Support → Level 2 Support → Manager
(Each level tries to handle or passes to next)
```

***

#### 5. Mediator Pattern

**Concept:** It's like having a central coordinator to facilitate communication between different parties. In a team project, instead of everyone talking directly to each other, everyone talks to a project manager (mediator), making the process smoother.

**Use Case:**

* Chat applications
* Air traffic control systems
* GUI dialog boxes
* Workflow engines

**How It Works:**

* Central mediator object handles communication
* Objects don't communicate directly
* Reduces dependencies between objects

**Example Scenario:**

```
Components (User A, User B, User C)
        ↓
    Mediator (ChatRoom)
        ↓
All communication flows through mediator
```

***

#### 6. State Pattern

**Concept:** This pattern is like changing your mood depending on the situation! The object can change its behavior based on its current state, without needing to rewrite the code for every situation.

**Use Case:**

* TCP connection states
* Document workflow (draft, review, published)
* Vending machines
* Game character states

**How It Works:**

* Object behavior changes when internal state changes
* Appears to change its class
* Perfect when an object has a lot of conditional behavior

**Example Scenario:**

```
States: Draft → Review → Approved → Published
Each state has different behavior for same operations
```

***

#### 7. Template Method Pattern

**Concept:** Think of this pattern like a recipe. It provides a general structure (template) for a process, but allows you to define some specific steps (like seasoning or garnish in cooking).

**Use Case:**

* Frameworks and libraries
* Data processing pipelines
* Game AI routines
* Database operations

**How It Works:**

* Defines skeleton of algorithm in base class
* Subclasses override specific steps
* Great way to ensure consistent flow while letting flexibility on the details

**Example Scenario:**

```
Template: Make Beverage
1. Boil water (same for all)
2. Brew (different: coffee vs tea)
3. Pour in cup (same for all)
4. Add condiments (different: sugar vs lemon)
```

***

#### 8. Iterator Pattern

**Concept:** It's like going through a line of items in a store. With this pattern, you can iterate through a collection of items, like a list or array, without needing to worry about the details of how the collection is structured.

**Use Case:**

* Collections (ArrayList, LinkedList, HashSet)
* File system traversal
* Database result sets
* Tree traversal

**How It Works:**

* Provides way to access elements sequentially
* Without exposing underlying representation
* Uniform interface for different collections

**Example Scenario:**

```
Iterator → next(), hasNext(), remove()
Works on: Arrays, Lists, Sets, Trees (same interface)
```

***

#### 9. Visitor Pattern

**Concept:** This pattern allows you to add new operations to existing objects without changing the objects themselves. It's like having a guest (visitor) who can come into your home and make improvements without altering the original design.

**Use Case:**

* Compiler operations (type checking, code generation)
* Document processing
* Shopping cart calculations
* Reporting systems

**How It Works:**

* Separate algorithm from object structure
* Add new operations without modifying classes
* Double dispatch technique

**Example Scenario:**

```
Elements (Document parts: Paragraph, Image, Table)
Visitors (SpellChecker, Printer, PDFExporter)
Each visitor can operate on all elements
```

***

#### 10. Memento Pattern

**Concept:** Imagine you want to save a game at a certain point and return to that point later. The memento pattern lets you capture and store an object's state, so you can revert back to it without exposing its internal details.

**Use Case:**

* Undo/redo functionality
* Save game states
* Transaction rollback
* History tracking

**How It Works:**

* Captures object's internal state
* Stores it externally
* Can restore to previous state
* Without exposing internal details

**Example Scenario:**

```
Originator (TextEditor) creates Memento (saved state)
Caretaker (History) stores Mementos
Can restore TextEditor to any saved state
```

***

### Quick Reference: Behavioral Patterns

| Pattern                     | Purpose                                  | Use When                                       | Example                        |
| --------------------------- | ---------------------------------------- | ---------------------------------------------- | ------------------------------ |
| **Observer**                | Notify multiple objects of state changes | One-to-many dependencies                       | Event listeners, Pub-Sub       |
| **Strategy**                | Select algorithm at runtime              | Multiple ways to perform operation             | Payment methods, Sorting       |
| **Command**                 | Encapsulate request as object            | Need undo/redo, queuing                        | GUI actions, Macros            |
| **Chain of Responsibility** | Pass request through chain               | Multiple handlers possible                     | Exception handling, Logging    |
| **Mediator**                | Centralize communication                 | Complex object interactions                    | Chat rooms, UI dialogs         |
| **State**                   | Change behavior based on state           | Object behaves differently in different states | TCP connections, Workflows     |
| **Template Method**         | Define algorithm skeleton                | Algorithm with varying steps                   | Data processing, Frameworks    |
| **Iterator**                | Access elements sequentially             | Need to traverse collections                   | Lists, Trees, Collections      |
| **Visitor**                 | Add operations without modifying classes | New operations on stable structure             | Compilers, Document processing |
| **Memento**                 | Capture and restore state                | Need undo/rollback                             | Text editors, Transactions     |

***

### Pattern Categories by Communication Type

#### One-to-Many Communication

* **Observer Pattern** - One subject notifies many observers

#### Request Handling

* **Chain of Responsibility** - Multiple handlers for a request
* **Command Pattern** - Encapsulate and queue requests

#### Centralized Communication

* **Mediator Pattern** - Central coordinator for multiple objects

#### Behavioral Variation

* **Strategy Pattern** - Select behavior at runtime
* **State Pattern** - Behavior changes with state
* **Template Method** - Customize algorithm steps

#### Traversal and Operations

* **Iterator Pattern** - Traverse collections
* **Visitor Pattern** - Perform operations on elements

#### State Management

* **Memento Pattern** - Save and restore state

***

### When to Use Behavioral Patterns

#### Use Behavioral Patterns When:

1. **Complex object interactions** - Many objects need to communicate
2. **Runtime behavior changes** - Behavior should be changeable at runtime
3. **Decoupling needed** - Want to reduce dependencies between objects
4. **Algorithm variations** - Multiple ways to perform an operation
5. **State management** - Object behavior depends on its state
6. **Notification systems** - Need to notify multiple objects of changes
7. **Request processing** - Requests need to be handled by multiple handlers

#### Benefits of Using Behavioral Patterns:

* **Loose coupling** - Objects are less dependent on each other
* **Flexibility** - Easy to add new behaviors
* **Maintainability** - Clear communication structure
* **Reusability** - Behaviors can be reused across objects
* **Scalability** - Easy to extend as system grows

***

### Comparison with Other Pattern Types

| Pattern Type   | Focus              | Examples                    |
| -------------- | ------------------ | --------------------------- |
| **Creational** | Object creation    | Singleton, Factory, Builder |
| **Structural** | Object composition | Adapter, Decorator, Facade  |
| **Behavioral** | Object interaction | Observer, Strategy, Command |

**Key Difference:**

* **Creational** → How to create objects
* **Structural** → How to compose objects
* **Behavioral** → How objects communicate and collaborate

***

### Real-World Analogies

| Pattern                     | Real-World Analogy                    |
| --------------------------- | ------------------------------------- |
| **Observer**                | Social media notifications            |
| **Strategy**                | Different payment methods at checkout |
| **Command**                 | Restaurant order system               |
| **Chain of Responsibility** | Customer support escalation           |
| **Mediator**                | Air traffic control                   |
| **State**                   | Traffic light system                  |
| **Template Method**         | Cooking recipe                        |
| **Iterator**                | TV channel surfing                    |
| **Visitor**                 | Home inspector visiting rooms         |
| **Memento**                 | Video game save points                |

***

### Summary

These behavioral patterns are the perfect tools to make object communication easier and more efficient. Whether you need to streamline interactions, organize responsibilities, or make systems more flexible, these patterns provide the structure and adaptability to handle it all!

#### Key Takeaways

**Core Concept:**

* Behavioral patterns focus on object communication and interaction
* Define how objects collaborate to accomplish tasks
* Manage control flow between objects

**Main Benefits:**

* **Clearer Communication** - Structured, organized interactions
* **Decoupling** - Objects don't need to know each other intimately
* **Flexibility** - Easy to change behaviors without modifying classes
* **Better Organization** - Clear structure for growing codebases

**10 Essential Patterns:**

1. **Observer** - Notify dependents of changes
2. **Strategy** - Interchangeable algorithms
3. **Command** - Encapsulate requests
4. **Chain of Responsibility** - Sequential request handling
5. **Mediator** - Centralized communication
6. **State** - Behavior based on state
7. **Template Method** - Algorithm skeleton
8. **Iterator** - Sequential access
9. **Visitor** - Add operations without modification
10. **Memento** - Capture and restore state

**When to Use:**

* Complex object interactions
* Need for runtime flexibility
* Want to reduce coupling
* Multiple algorithm variations
* State-dependent behavior

***

### Conclusion

Behavioral Design Patterns are a great way to keep your code clean, efficient, and adaptable. They focus on how objects interact, ensuring smooth communication while reducing dependencies.

Whether you're dealing with:

* Real-time systems
* Complex applications
* Notification systems
* Workflow management
* State machines
* Algorithm variations

These patterns provide flexible, modular, and scalable solutions.

**Remember:** Just like how you organize a fun group chat with your friends, behavioral patterns help objects in your code communicate more effectively and stay organized, leading to better software that's easier to maintain and grow!

By mastering behavioral patterns, you gain powerful tools for:

* Managing complex interactions
* Creating flexible, maintainable code
* Building scalable systems
* Improving code organization
* Reducing coupling and dependencies

***

### Next Steps

Continue your learning journey by exploring:

* Detailed implementation of each behavioral pattern
* Combining multiple patterns for complex scenarios
* Real-world case studies of behavioral patterns
* Anti-patterns to avoid in object communication
* Design pattern relationships and interactions
* Advanced behavioral pattern techniques
