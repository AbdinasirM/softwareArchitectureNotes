# Understanding Layered Architecture

**Layered Architecture** is a way to structure applications by dividing them into multiple layers. Each layer has a specific responsibility and only communicates with the layer directly below it. This separation helps organize code and makes it easier to maintain and understand.

---

## How Does Layered Architecture Work?

- Each layer is responsible for a specific task.
- A layer **can call the layer below it** but cannot call layers above it.
- For example, the Presentation Layer (UI) can talk to the Application Layer but cannot directly talk to the Business Layer.

---

### Typical Layers in a Layered Architecture

There are usually five layers in a traditional layered architecture:

1. **Presentation Layer**:
   - Handles the user interface (UI).
   - Displays information to the user and collects input.
   - Example: A web page or mobile app screen.

2. **Application Layer**:
   - Acts as a bridge between the UI and the Business Layer.
   - Processes user input and sends it to the Business Layer.
   - Example: Converts user data from a form into a format the Business Layer can understand.

3. **Business Layer**:
   - Contains the core business logic.
   - Handles decisions and calculations based on business rules.
   - Example: Calculates discounts or checks if a user is eligible for a loan.

4. **Persistence Layer**:
   - Contains code for interacting with the database.
   - Handles saving, updating, and retrieving data.
   - Example: SQL queries or ORM (Object-Relational Mapping) code.

5. **Data Layer**:
   - The actual database where data is stored.
   - Example: A SQL or NoSQL database like PostgreSQL or MongoDB.

---

### Diagram: Layered Architecture
```
+--------------------+
|  Presentation Layer|  (UI for user interaction)
+--------------------+
         |
         v
+--------------------+
|  Application Layer |  (Connects UI to business logic)
+--------------------+
         |
         v
+--------------------+
|   Business Layer   |  (Business rules and logic)
+--------------------+
         |
         v
+--------------------+
| Persistence Layer  |  (Database interaction code)
+--------------------+
         |
         v
+--------------------+
|    Data Layer      |  (Database itself)
+--------------------+
```

---

## Advantages of Layered Architecture

1. **Well-Known Among Developers**:
   - Most developers are familiar with this structure, making it easier to work in teams.

2. **Easy to Organize**:
   - Code is divided into clear sections based on responsibilities, improving readability and maintainability.

---

## Disadvantages of Layered Architecture

1. **Can Lead to Monolithic Applications**:
   - All layers are tightly connected, which can make the application harder to break into smaller parts for scaling.

2. **Lots of Code to Write**:
   - Passing data through multiple layers often requires writing boilerplate code, which can slow down development.

---

### Example Scenario: Online Store

Let’s consider how an **online store** might use layered architecture:

1. **Presentation Layer**:
   - Displays the product catalog and handles user actions like adding items to the cart.

2. **Application Layer**:
   - Processes the "Add to Cart" request and passes it to the Business Layer.

3. **Business Layer**:
   - Checks if the product is in stock and calculates the total price.

4. **Persistence Layer**:
   - Updates the database to reflect the items in the user’s cart.

5. **Data Layer**:
   - The database stores the product inventory and cart details.

---

### Diagram: Online Store Example
```
+----------------------------+
| Presentation Layer         |  User clicks "Add to Cart"
+----------------------------+
          |
          v
+----------------------------+
| Application Layer          |  Translates user request
+----------------------------+
          |
          v
+----------------------------+
| Business Layer             |  Checks stock, calculates price
+----------------------------+
          |
          v
+----------------------------+
| Persistence Layer          |  Saves cart info in database
+----------------------------+
          |
          v
+----------------------------+
| Data Layer                 |  Database stores cart details
+----------------------------+
```

---

## When to Use Layered Architecture?

Layered Architecture is ideal for:
- Applications with clear separations of responsibility, like CRUD (Create, Read, Update, Delete) apps.
- Teams looking for a simple, well-known structure to organize their code.

---

### Comparison: Layered vs. Other Architectures

| Feature                  | Layered Architecture             | Microservices Architecture       |
|--------------------------|----------------------------------|-----------------------------------|
| **Structure**            | Divided into layers              | Divided into independent services |
| **Scalability**          | Harder to scale                 | Easier to scale                  |
| **Code Organization**    | Organized by functionality       | Organized by business domains    |
| **Maintenance**          | Easy to maintain small projects | Better for large projects        |
