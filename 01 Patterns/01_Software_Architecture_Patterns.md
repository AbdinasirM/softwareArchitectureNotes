# Patterns in Software Development

A **pattern** is like a recipe for solving a common problem in software development. Patterns help developers write code that is easy to understand, change, and reuse.

---

## Examples of Common Design Patterns

### 1. Repository Pattern
The Repository Pattern separates the way we interact with the database from the rest of the application. This makes it easy to change the database later without affecting the rest of the code.

#### Simple Explanation:
Imagine a library where you can borrow books without needing to know how they’re stored. The librarian (repository) handles all that for you.

#### Diagram:
```
+---------------------+      +----------------+
| Application Logic   | ---> | Repository     |
+---------------------+      +----------------+
                                  |
                                  v
                         +----------------+
                         | Database       |
                         +----------------+
```

#### Code Example:
```python
# Repository handles data retrieval
class UserRepository:
    def get_user_by_id(self, user_id):
        # Imagine this gets data from a database
        return {"id": user_id, "name": "John Doe"}

# Application logic uses the repository
class UserService:
    def __init__(self, user_repository):
        self.user_repository = user_repository

    def get_user(self, user_id):
        return self.user_repository.get_user_by_id(user_id)

# Example usage
repo = UserRepository()
service = UserService(repo)
print(service.get_user(1))  # Output: {'id': 1, 'name': 'John Doe'}
```

---

### 2. Singleton Pattern
The Singleton Pattern makes sure a class has only **one instance** and gives everyone access to that same instance.

#### Simple Explanation:
Think of it like a printer in an office. Everyone uses the same printer, not a new one for each person.

#### Diagram:
```
+----------------------+
|       Singleton      |
| (One Instance Only)  |
+----------------------+
         ^
         |
  +---------------+
  | Application   |
  +---------------+
```

#### Code Example:
```python
class Singleton:
    _instance = None

    @staticmethod
    def get_instance():
        if Singleton._instance is None:
            Singleton._instance = Singleton()
        return Singleton._instance

# Example usage
singleton1 = Singleton.get_instance()
singleton2 = Singleton.get_instance()
print(singleton1 is singleton2)  # Output: True (Both are the same instance)
```

---

### 3. Builder Pattern
The Builder Pattern is used to create complex objects step by step, so the process is easy to follow.

#### Simple Explanation:
Think of building a sandwich. You add bread, lettuce, meat, and sauce step by step, instead of doing it all at once.

#### Diagram:
```
+------------------+          +---------------+
|    Builder       | <------- | Application   |
+------------------+          +---------------+
         |
         v
+------------------+
| Complete Object  |
+------------------+
```

#### Code Example:
```python
# The object to build
class House:
    def __init__(self):
        self.walls = None
        self.roof = None

# The builder class
class HouseBuilder:
    def __init__(self):
        self.house = House()

    def build_walls(self, wall_type):
        self.house.walls = wall_type
        return self

    def build_roof(self, roof_type):
        self.house.roof = roof_type
        return self

    def get_house(self):
        return self.house

# Example usage
builder = HouseBuilder()
house = builder.build_walls("Brick Walls").build_roof("Tile Roof").get_house()
print(f"House with {house.walls} and {house.roof}")
```

---

### 4. Factory Pattern
The Factory Pattern is a way to create objects without directly specifying their exact class.

#### Simple Explanation:
Think of a bakery where you order "cake" and the bakery makes it for you. You don’t need to know how the cake is made, you just get it.

#### Diagram:
```
+------------------+
|    Factory       |
+------------------+
         |
         v
+------------------+
| Product (Object) |
+------------------+
```

#### Code Example:
```python
# Parent class
class Animal:
    def speak(self):
        pass

# Child classes
class Dog(Animal):
    def speak(self):
        return "Woof!"

class Cat(Animal):
    def speak(self):
        return "Meow!"

# Factory class
class AnimalFactory:
    @staticmethod
    def create_animal(animal_type):
        if animal_type == "dog":
            return Dog()
        elif animal_type == "cat":
            return Cat()

# Example usage
animal = AnimalFactory.create_animal("dog")
print(animal.speak())  # Output: Woof!
```

---

## Why Use Software Architecture Patterns?

Software architecture patterns help developers plan how to build applications. They make software:

- **Easier to build**: Patterns give a clear plan.
- **Easier to maintain**: The code is well-organized and modular.
- **Easier to scale**: The system can grow without breaking.

---

## Design Patterns vs. Architecture Patterns

| **Feature**               | **Design Patterns**              | **Architecture Patterns**         |
|---------------------------|----------------------------------|-----------------------------------|
| **Scope**                 | Small, specific problems         | Large, system-wide organization  |
| **Purpose**               | Focus on solving specific tasks  | Focus on structuring the system  |
| **Components**            | Small parts of the app           | Many parts working together      |
| **Paradigm Independence** | Works with any programming style | Works across programming styles  |

*Paradigm independence* means these patterns can work whether you're using object-oriented programming, functional programming, or any other style.

