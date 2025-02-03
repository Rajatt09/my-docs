# Contents of the file: /documentation-project/documentation-project/software-engineering/basics/design-patterns.md

Design Patterns in Software Engineering
========================================

Design patterns are standard solutions to common problems in software design. They represent best practices that can be applied to various situations. Here are some of the most common design patterns:

1. **Singleton Pattern**
   - Ensures that a class has only one instance and provides a global point of access to it.
   - Useful when exactly one object is needed to coordinate actions across the system.

2. **Factory Pattern**
   - Defines an interface for creating an object but allows subclasses to alter the type of objects that will be created.
   - Useful for managing and maintaining a large number of related classes.

3. **Observer Pattern**
   - A one-to-many dependency between objects so that when one object changes state, all its dependents are notified and updated automatically.
   - Commonly used in event handling systems.

4. **Strategy Pattern**
   - Enables selecting an algorithm's behavior at runtime.
   - Useful for defining a family of algorithms, encapsulating each one, and making them interchangeable.

5. **Decorator Pattern**
   - Allows behavior to be added to individual objects, either statically or dynamically, without affecting the behavior of other objects from the same class.
   - Useful for adhering to the Single Responsibility Principle.

6. **Command Pattern**
   - Encapsulates a request as an object, thereby allowing for parameterization of clients with queues, requests, and operations.
   - Useful for implementing undoable operations.

These patterns help in creating more flexible and reusable code, making it easier to manage and scale software applications.