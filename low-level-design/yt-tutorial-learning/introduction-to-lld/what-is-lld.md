# What is LLD

## Low-Level System Design Guide

### Overview

Low-Level Design (LLD) is a critical phase in the software development process that focuses on designing the individual components outlined in High-Level Design (HLD). LLD delves into the specifics, defining how modules, classes, functions, and data structures interact to achieve the desired functionality.

> **Example:** In a movie ticket booking system, LLD details how components like seat selection, payment processing, and ticket generation are implemented and interact with one another.

***

### LLD vs HLD: Understanding the Difference

Low-Level Design (LLD) and High-Level Design (HLD) are two complementary stages in software development, each focusing on different levels of detail.

#### High-Level Design (HLD)

HLD focuses on the **overall architecture** of the system. It defines the main components, their interactions, and integration points.

**Key Components:**

* **User Interface**: Where users interact with the system
* **Backend Services**: Business logic and processing
* **Database**: Data storage and management
* **External Services**: Third-party integrations (e.g., payment gateways)

**Example - Movie Booking System HLD:**

In a movie ticket booking system, HLD outlines:

* User interface for movie and seat selection
* Backend services handling booking requests and seat availability
* Database storing movie schedules, user data, and bookings
* Integration with payment gateway services

**Focus:** Architecture, component relationships, and data flow between major system parts.

***

#### Low-Level Design (LLD)

LLD dives into the **implementation specifics** of individual features. It provides detailed blueprints for each component.

**Key Elements:**

* **Workflows**: Step-by-step process flows
* **Data Validation**: Input verification and constraint rules
* **Algorithms**: Business logic implementation details
* **Database Schemas**: Table structures, fields, and relationships
* **Error Handling**: Edge cases and exception management

**Example - Booking Process LLD:**

For the ticket booking feature, LLD specifies:

1. User selects movie and showtime
2. System validates seat availability in real-time
3. Selected seats are temporarily locked (prevent double booking)
4. Payment details are validated and processed
5. Booking record is created in database with transaction details
6. Confirmation message is generated and sent via email/SMS
7. Seats are permanently marked as booked

**Focus:** Implementation precision, algorithms, and technical details for each feature.

***

#### Key Differences Summary

| Aspect           | High-Level Design (HLD)  | Low-Level Design (LLD)     |
| ---------------- | ------------------------ | -------------------------- |
| **Scope**        | System architecture      | Component implementation   |
| **Detail Level** | Broad overview           | Detailed specifications    |
| **Focus**        | What components exist    | How components work        |
| **Output**       | Architecture diagrams    | Class diagrams, algorithms |
| **Audience**     | Architects, stakeholders | Developers, engineers      |

> **Remember:** HLD sets the vision for the system, while LLD ensures every feature is implemented accurately and aligns with the high-level plan.

***

### Building Blocks of LLD

#### 1. Requirement Gathering

Understand the detailed requirements of the system, including functionality, constraints, and edge cases to ensure the design meets user needs.

**For a Movie Ticket Booking System:**

* Seat selection mechanism
* Payment processing integration
* Ticket generation and validation
* Handling simultaneous bookings for the same seat
* Cancellation and refund logic
* Notification system (email/SMS)

***

#### 2. Laying Down Use Cases

Define specific scenarios that the system will handle, outlining inputs, actions, and expected outputs. Use cases help clarify scope and guide the design process.

**Common Use Cases:**

**Use Case 1: Book Movie Tickets**

* Actor: Customer
* Input: Movie selection, showtime, seat numbers, payment details
* Output: Booking confirmation, ticket details

**Use Case 2: Handle Group Bookings**

* Actor: Customer
* Input: Multiple seats with proximity preference
* Output: Adjacent or nearby seats allocated

**Use Case 3: Cancel Booking**

* Actor: Customer
* Input: Booking ID, cancellation reason
* Output: Cancellation confirmation, refund initiated

**Use Case 4: Send Notifications**

* Actor: System
* Input: Booking confirmation details
* Output: Email/SMS sent to customer

***

#### 3. UML Diagrams

Create diagrams to visually represent the structure, behavior, and interactions of system components.

**Common UML Diagrams in LLD:**

**Class Diagram**

Represents entities and their relationships.

**Key Classes for Movie Booking System:**

* `User`: Customer information and booking history
* `Movie`: Movie details (title, genre, duration, rating)
* `Theater`: Theater information and screens
* `Show`: Specific screening (movie, time, screen)
* `Seat`: Individual seat details and status
* `Booking`: Booking transaction details
* `Payment`: Payment information and status
* `Ticket`: Generated ticket with QR code

**Sequence Diagram**

Shows the flow of actions and interactions over time.

**Booking Flow Example:**

1. User → System: Select movie and showtime
2. System → Database: Check seat availability
3. Database → System: Return available seats
4. User → System: Select seats
5. System → Seat: Lock selected seats
6. User → System: Provide payment details
7. System → Payment Gateway: Process payment
8. Payment Gateway → System: Payment confirmed
9. System → Database: Create booking record
10. System → Notification Service: Send confirmation
11. System → User: Display booking confirmation

**Activity Diagram**

Maps the workflow and decision points in processes.

**Booking Workflow:**

* Start → Select Movie → Choose Showtime → Select Seats
* Check Availability → \[Available] Continue / \[Not Available] Select Different Seats
* Lock Seats → Enter Payment Details → Process Payment
* \[Success] Generate Ticket → Send Notification → End
* \[Failure] Release Seats → Show Error → End

***

#### 4. Model Problems Using Design Patterns

This phase focuses on solving specific design challenges using proven design patterns. Design patterns provide reusable solutions to common problems.

**Common Design Patterns in LLD:**

**Factory Pattern**

Creates objects without specifying exact classes.

**Example:** Creating different types of tickets (Standard, Premium, VIP) based on seat category.

**Strategy Pattern**

Defines a family of algorithms and makes them interchangeable.

**Example:** Different payment strategies (Credit Card, Debit Card, UPI, Wallet).

**Observer Pattern**

Notifies multiple objects about state changes.

**Example:** Notifying users about seat availability updates or booking confirmations.

**Singleton Pattern**

Ensures only one instance of a class exists.

**Example:** Database connection manager or configuration handler.

**State Pattern**

Allows objects to change behavior based on internal state.

**Example:** Booking states (Pending, Confirmed, Cancelled, Refunded).

***

#### 5. Implement Code

Translate the design into clean, modular, and efficient code following best practices and design principles.

**Key Principles:**

**SOLID Principles**

* **S**ingle Responsibility: Each class has one purpose
* **O**pen/Closed: Open for extension, closed for modification
* **L**iskov Substitution: Subtypes must be substitutable for base types
* **I**nterface Segregation: Many specific interfaces over one general interface
* **D**ependency Inversion: Depend on abstractions, not concretions

**DRY (Don't Repeat Yourself)**

Avoid code duplication by extracting common functionality.

**KISS (Keep It Simple, Stupid)**

Prefer simple solutions over complex ones.

**YAGNI (You Aren't Gonna Need It)**

Don't add functionality until it's necessary.

**Code Quality Standards:**

* Clear and descriptive naming conventions
* Comprehensive error handling
* Proper logging and monitoring
* Unit tests for all components
* Code comments for complex logic
* Consistent formatting and style

***

### Best Practices for LLD

1. **Start Simple**: Begin with core functionality before adding complexity
2. **Think Scalability**: Design with future growth in mind
3. **Document Thoroughly**: Maintain clear documentation for all components
4. **Review Regularly**: Conduct design reviews with team members
5. **Iterate and Refine**: Continuously improve the design based on feedback
6. **Consider Edge Cases**: Plan for error scenarios and boundary conditions
7. **Maintain Consistency**: Use consistent naming and design patterns throughout

***

### Conclusion

Low-Level Design (LLD) is an essential phase in the software development lifecycle that translates high-level architectural concepts into detailed specifications for individual components. By focusing on modularity, clear interface definitions, and following design principles like SOLID and DRY, LLD ensures that software systems are robust, maintainable, and scalable.

A well-executed LLD serves as a comprehensive blueprint for developers, reducing ambiguity during implementation and facilitating easier maintenance and future enhancements.

***

### Additional Resources

* **Design Patterns**: Gang of Four (GoF) Design Patterns
* **UML Modeling**: Unified Modeling Language specifications
* **Clean Code**: Robert C. Martin's principles
* **System Design**: System Design Interview resources

***

**Last Updated:** 2025
