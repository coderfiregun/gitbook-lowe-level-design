# How to approach LLD

## How to Approach LLD Problems

### Overview

Low-Level Design (LLD) problems are a critical component of technical interviews, especially for backend engineering roles. They evaluate your ability to design software systems at a detailed level, focusing on class structures, design patterns, relationships, and implementation details.

This guide provides a systematic approach to tackle LLD problems effectively, using a movie ticket booking system as a practical example.

***

### Step-by-Step Approach

#### Step 1: Clarify Requirements and Use Cases

The interview begins with the problem statement. Your first task is to clarify requirements and establish a shared understanding with the interviewer.

**Example Conversation**

**Interviewer:** "Design a movie ticket booking system."

**You:** "Absolutely! Based on the problem, here's my understanding:

* Users can browse theaters, select movies or shows, book seats, and make payments
* The system needs to handle concurrent bookings efficiently

Would you like me to add any details to this understanding?"

**Interviewer:** "That's a good summary. We can move ahead."

**You:** "To clarify further:

* Should we support multiple user types, like admins and customers?
* How should we handle seat availability during concurrent bookings?
* Is payment processing and ticket generation included in scope?"

**Interviewer:** "Yes, concurrency and payment are key. Admin roles and advanced features are out of scope for now."

**You:** "Understood. Here's the core flow I'll focus on:

1. Users search for movies based on location
2. Movies are mapped to screens, and screens to theaters
3. Seats are selected and locked for booking
4. Payment processing confirms the booking

Does this cover the main use cases?"

**Interviewer:** "Yes, that looks great. Proceed ahead."

> **Pro Tip:** Always write down key points discussed with the interviewer. This helps maintain clarity and ensures you address the critical aspects of the problem.

***

#### Step 2: Identify Entities (Classes)

Break the system down into core entities. Focus on the main nouns in the problem domain.

**You:** "Based on the requirements, I've identified these core entities:

* **User** - Customers who book tickets
* **Movie** - Movie information
* **Theater** - Cinema complex with multiple screens
* **Screen** - Individual screening rooms
* **Show** - Specific movie screening at a time
* **Seat** - Individual seats with status
* **Booking** - Ticket booking transaction
* **Payment** - Payment information and status"

**Interviewer:** "Yes, that looks great. Proceed ahead."

> **Pro Tip:** Avoid excessive entity details as they consume time better spent explaining the core problem's solution.

***

#### Step 3: Define Relationships Between Entities

Map out how entities interact and relate to each other.

**You:** "Here's how the entities are related:

1. A **Theater** has multiple **Screens**, each linked to specific **Seats**
2. A **Show** occurs on a specific **Screen** and maps to a **Movie**
3. A **Seat** is tied to a **Show** for tracking availability during bookings
4. A **Booking** associates a **User** with **Seats**, **Show**, and **Payment**"

**Example: Show Class**

```java
public class Show {
    private final String id;
    private final Movie movie;
    private final Screen screen;
    private final Date startTime;
    private final Integer durationInMinutes;
}
```

**Key Point:** A Show is uniquely associated with a specific Movie and Screen.

**Example: Theater and Screen**

```java
public class Theater {
    private final String id;
    private final String name;
    private final String location;
    private final List<Screen> screens;
}

public class Screen {
    private final String id;
    private final String name;
    private final List<Seat> seats;
}
```

**Key Point:** A Theater contains multiple Screens, and each Screen manages its Seats.

**Example: Booking and Payment**

```java
public class Booking {
    private final String id;
    private final User user;
    private final Show show;
    private final List<Seat> bookedSeats;
    private final Payment payment;
}

public class Payment {
    private final String id;
    private final double amount;
    private final PaymentStatus status;
    private final Date timestamp;
}
```

**Key Point:** A Booking includes User, Show, and Seats, and is linked to a Payment to track transaction status.

**Interviewer:** "Yes, this is aligned. Please proceed ahead."

***

#### Step 4: Identify Core Methods for Each Class

Focus on critical methods that drive the system's functionality.

**You:** "Moving on to the primary functionalities, I'll focus on the major methods critical to the system:

**Seat Management**

* `lockSeats(List<Seat> seats, int showId)` – Locks selected seats for a user, preventing others from booking them during the session
* `releaseSeats(List<Seat> seats, int showId)` – Releases previously locked seats if the booking is canceled or not confirmed

**Booking Management**

* `createBooking(int userId, int showId, List<Integer> seatIds)` – Creates a new booking for the user with the selected seats
* `cancelBooking(int bookingId)` – Cancels a booking and releases the locked seats

**Concurrency Handling**

To manage concurrency, we can use:

* Synchronized blocks or distributed locks to ensure multiple users cannot lock the same seats simultaneously
* Retry mechanism (e.g., exponential backoff) for seat locking failures

**Design Patterns**

* **Strategy Pattern** for handling different payment methods (credit card, wallet, etc.) without modifying booking logic
* **Factory Pattern** to create different types of bookings (VIP, Regular, etc.) based on user preferences or seat categories"

**You:** "Would you like me to dive deeper into any particular functionality?"

**Interviewer:** "Let's focus on the lockSeats and createBooking methods."

> **Pro Tip:** Focus on implementing core business logic rather than basic CRUD operations. Interviewers primarily evaluate your approach to designing and implementing complex system functionalities.

***

#### Step 5: Implement Necessary Methods

Demonstrate clean, maintainable code following design principles like SOLID, DRY, KISS, and YAGNI.

**You:** "I'll begin with the lockSeats method. Would you prefer I explain the approach first or code while explaining?"

**Interviewer:** "You may code and explain simultaneously."

**You:** "I'll proceed with the implementation."

**Implementation: Lock Seats**

```java
public boolean lockSeats(List<Integer> seatIds, int showId, int userId) {
    synchronized (this) {
        for (int seatId : seatIds) {
            Seat seat = seatRepository.getSeat(seatId, showId);
            if (seat.getStatus() != SeatStatus.AVAILABLE) {
                return false; // Seat already locked or booked
            }
            seat.setStatus(SeatStatus.LOCKED);
            seat.setLockedBy(userId); // Associate the locked seat with the user ID
            seatRepository.updateSeat(seat);
        }
    }
    return true;
}
```

**Explanation:** Using synchronized block to prevent race conditions. If any seat is unavailable, the entire operation fails to maintain atomicity.

**Interviewer:** "We can proceed with the createBooking() method implementation now."

**Implementation: Create Booking**

```java
public Booking createBooking(final String userId, final Show show, final List<Seat> seats) {
    // Check if any seat is already booked
    if (isAnySeatAlreadyBooked(show, seats)) {
        throw new SeatPermanentlyUnavailableException();
    }
    
    // Attempt to lock the seats for the user
    boolean lockSuccess = seatLockProvider.lockSeats(seats, show.getId(), userId);
    if (!lockSuccess) {
        throw new SeatLockFailedException("Failed to lock seats for the user");
    }
    
    // Generate a unique booking ID
    final String bookingId = UUID.randomUUID().toString();
    final Booking newBooking = new Booking(bookingId, show, userId, seats);
    
    // Store the booking
    showBookings.put(bookingId, newBooking);
    
    // Return the new booking
    return newBooking;
}
```

**Explanation:** Validates seat availability, locks seats, creates booking, and handles failures with appropriate exceptions.

***

#### Step 6: Exception Handling

Incorporate error handling to manage edge cases gracefully.

**Example: No Seats Available**

Ensure users are informed when attempting to book already reserved seats.

```java
private boolean isAnySeatAlreadyBooked(final Show show, final List<Seat> seats) {
    final List<Seat> bookedSeats = getBookedSeats(show);
    for (Seat seat : seats) {
        if (bookedSeats.contains(seat)) {
            return true;
        }
    }
    return false;
}

public Booking createBooking(final String userId, final Show show, final List<Seat> seats) {
    if (isAnySeatAlreadyBooked(show, seats))
        throw new SeatPermanentlyUnavailableException();
    // rest of the logic
}
```

**Example: Payment Failure**

Handle failed transactions and provide retry options.

```java
public void processPaymentFailed(final Booking booking, final String user) {
    if (!booking.getUser().equals(user)) {
        throw new BadRequestException();
    }
    
    if (!bookingFailures.containsKey(booking)) {
        bookingFailures.put(booking, 0);
    }
    
    final Integer currentFailuresCount = bookingFailures.get(booking);
    final Integer newFailuresCount = currentFailuresCount + 1;
    bookingFailures.put(booking, newFailuresCount);
    
    if (newFailuresCount > allowedRetries) {
        seatLockProvider.unlockSeats(booking.getShow(), booking.getSeatsBooked(), booking.getUser());
    }
}
```

**Explanation:** Tracks payment failures and releases seats after exceeding retry limit.

***

### Key Takeaways

#### 1. Systematic Progression

* Begin with thorough requirement gathering
* Move systematically from high-level entities to detailed implementations
* Validate your approach at each step with the interviewer

#### 2. Practical Considerations

* Focus on maintainable and scalable solutions
* Address critical aspects like concurrency and error handling
* Demonstrate knowledge of design patterns where relevant

#### 3. Communication Excellence

* Clearly articulate your design choices
* Explain tradeoffs in your decisions
* Show adaptability when receiving interviewer feedback

***

### What Makes a Successful LLD Interview

A successful LLD interview is not about creating a perfect design in the first attempt. It's about demonstrating:

* **Structured Thinking**: Systematic approach to problem-solving
* **Translation Skills**: Converting requirements into concrete solutions
* **OOP Knowledge**: Understanding of object-oriented design principles
* **Clean Code**: Writing maintainable, readable code
* **Adaptability**: Openness to feedback and ability to iterate

By following this systematic approach and maintaining clear communication throughout the interview, you'll be well-equipped to tackle any Low-Level Design challenge effectively.

***

### Additional Resources

* Design Patterns: Gang of Four (GoF) Design Patterns
* SOLID Principles: Clean Code by Robert C. Martin
* System Design: System Design Interview books and resources

***

**Last Updated:** 2025
