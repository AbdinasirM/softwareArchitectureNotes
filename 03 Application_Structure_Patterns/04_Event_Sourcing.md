# Understanding Event Sourcing

**Event Sourcing** is a design pattern where an application stores a **sequence of events** (things that happened in the past) instead of just the current state of the system. These events are used to rebuild or "rehydrate" the current state of the system whenever needed.

---

## Key Concept: Events, Not State

- **Event**: A record of something that happened in the system.
  - Example: "User registered," "Product added to cart," or "Payment processed."
  
- **Rehydration/Replay**: The process of rebuilding the current state by replaying all stored events.

---

### How Event Sourcing Works

1. **Capture Events**:
   - When something happens (e.g., an order is placed), the system records it as an event.

2. **Store Events**:
   - Events are stored in an **event store**, a special type of database designed for event sourcing.

3. **Rebuild State**:
   - To get the current state, replay all stored events in sequence.

---

### Diagram: Event Sourcing Workflow
```
+-----------------------------+
|        Application          |
+-----------------------------+
           |
           v
+-----------------------------+
|      Event Store            |
| - Event 1: User Registered  |
| - Event 2: Added to Cart    |
| - Event 3: Payment Processed|
+-----------------------------+
           |
           v
+-----------------------------+
|      Rehydrated State       |
| - Order: Completed          |
| - Cart: Empty               |
+-----------------------------+
```

---

## Advantages of Event Sourcing

1. **Trace of Events**:
   - Every change is stored as an event, providing a full history of what happened.

   #### Example:
   - You can see exactly how a user's order went from "created" to "shipped."

2. **Audit Trail**:
   - Perfect for industries like finance or healthcare where tracking changes is critical.

3. **Business Language**:
   - Events are written in terms that match business actions (e.g., "Order Placed"), making them easier to understand.

4. **Event Replay**:
   - You can replay events to debug issues or rebuild the system's state after an error or update.

---

## Disadvantages of Event Sourcing

1. **Replay and External Systems**:
   - Replaying events to external systems (e.g., reporting tools) can be slow and require additional logic.

2. **Event Structure Changes**:
   - If the format of stored events changes, it can break existing functionality unless carefully managed.

3. **Snapshots**:
   - Replaying all events every time can be slow for large datasets. Periodic **snapshots** (saved intermediate states) can mitigate this but add complexity.

---

### Example Scenario: E-Commerce Platform

An **e-commerce platform** using Event Sourcing might record the following events for an order:

1. **Events**:
   - "Order Created"
   - "Item Added to Cart"
   - "Payment Completed"
   - "Order Shipped"

2. **Current State**:
   - By replaying the events, the system determines:
     - Order Status: "Shipped"
     - Payment: "Completed"
     - Cart: "Empty"

---

### Diagram: Event Sourcing in E-Commerce
```
+----------------------------+
| Event Store                |
| - Event 1: Order Created   |
| - Event 2: Item Added      |
| - Event 3: Payment Done    |
| - Event 4: Order Shipped   |
+----------------------------+
           |
           v
+----------------------------+
| Rehydrated State           |
| - Order Status: Shipped    |
| - Payment: Completed       |
| - Cart: Empty              |
+----------------------------+
```

---

## When to Use Event Sourcing?

Event Sourcing is ideal for:
- Systems that need a full history of changes (e.g., auditing or compliance).
- Applications requiring **debugging or replaying** past states.
- Use cases with complex workflows that benefit from step-by-step event tracking.

---

### Comparison: Event Sourcing vs. Traditional State Storage

| Feature                   | Event Sourcing                     | Traditional State Storage        |
|---------------------------|-------------------------------------|----------------------------------|
| **Data Storage**          | Stores all events                  | Stores only the current state    |
| **Traceability**          | Full history of changes            | No history, only the latest state|
| **Performance**           | Can require snapshots for speed    | Faster for small-scale systems   |
| **Complexity**            | Higher due to replay and snapshots | Simpler to implement             |

