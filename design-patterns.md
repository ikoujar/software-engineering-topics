# Design patterns

## what's design patters?:

- Design pattern are typical solutions to commonly occurring problems in software design.
- They are like pre-made blueprints that you can customize tp solve a recurring design problem in your code.

You can’t just find a pattern and copy it into your program, the way you can with off-the-shelf functions or libraries. The pattern is not a specific piece of code, but a general concept for solving a particular problem. You can follow the pattern details and implement a solution that suits the realities of your own program.

BookName: Gang of Four.

## Design patterns categories:
- Creational Pattern (Different ways to create objects)
- Structural Patterns (Organizing the relation between objects)
- Behaviour Patterns (Communications between objects)

## Benefits of the design patterns:
- Communicate with other developer on more abstract level (e.g. you can use the pattern name to explain the idea, instead of writing code trying to explain it like if its new thing)
- It makes you a better designer, you will learn how to write reusable, maintainable and extensible software, no matter the language or the technology that you use.
- Helps you learn and use new frameworks faster, because behind each framework there is a specific or multiple patterns so the difference is only kind of a syntax and sme rules for that framework and language.


## Strategy Pattern:

Duck class inheritance problem.

- Is-a: means a class inherits from another class
- Has-a (Composition)

The main problem in the strategy pattern is changes.

### Overview
The Strategy Pattern is a behavioral design pattern described in the book "Design Patterns: Elements of Reusable Object-Oriented Software" by the Gang of Four (GoF).
It allows different algorithms or behaviors to be selected at runtime based on a specific context. It encapsulates a family of related algorithms and makes them interchangeable without changing the context in which they are used.
This pattern promotes open-closed principle, as it allows for new behaviors to be added to the system without modifying the existing code.

### When to use

- When different variations of an algorithm or behavior are required within the same system
- When there is a need to switch between algorithms or behaviors dynamically at runtime
- When there is a need to decouple an algorithm from its context

### Advantages
- Encapsulation of algorithms: The Strategy Pattern allows algorithms to be encapsulated into separate classes, which makes them easier to maintain, test, and reuse.
- Flexibility: The pattern provides flexibility by allowing the algorithm to be changed at runtime, without requiring any changes to the client code.
- Easy to switch algorithms: The pattern makes it easy to switch between different algorithms, as they can be implemented as separate classes and easily swapped out.
- Reduced code duplication: By encapsulating algorithms into separate classes, the pattern can reduce code duplication and improve the overall structure of the codebase.


### Disadvantages
- Increased complexity: The pattern can introduce additional complexity to the codebase, as it requires the creation of multiple classes to encapsulate the different algorithms.
- Performance overhead: The use of the Strategy Pattern can result in additional performance overhead, as it requires runtime decisions about which algorithm to use.
- Increased memory usage: The use of multiple classes can increase the memory usage of the application, which may be a concern in resource-constrained environments.
- Dependency injection: The pattern may require the use of dependency injection to manage the relationships between the different classes, which can introduce additional complexity.

### The bottom line
Overall, the advantages of the Strategy Pattern typically outweigh its disadvantages, and it can be a powerful tool for managing complex algorithms in an object-oriented codebase.

### Example
```typescript
// Define the interface that all strategies must implement.
interface Strategy {
  doAlgorithm(data: string[]): string[];
}

// Concrete strategy that sorts the data in ascending order.
class ConcreteStrategyA implements Strategy {
  public doAlgorithm(data: string[]): string[] {
    return data.sort();
  }
}

// Concrete strategy that sorts the data in descending order.
class ConcreteStrategyB implements Strategy {
  public doAlgorithm(data: string[]): string[] {
    return data.sort().reverse();
  }
}

// Context that uses a strategy to perform an algorithm.
class Context {
  private strategy: Strategy;

  constructor(strategy: Strategy) {
    this.strategy = strategy;
  }

  // Set a new strategy for the context.
  public setStrategy(strategy: Strategy): void {
    this.strategy = strategy;
  }

  // Use the strategy to perform an algorithm on some data.
  public doSomeBusinessLogic(): void {
    const data = ["a", "b", "c", "d", "e"];
    const result = this.strategy.doAlgorithm(data);
    console.log(result.join(","));
  }
}

// Usage example
const context = new Context(new ConcreteStrategyA());
console.log("Client: Strategy is set to normal sorting.");
context.doSomeBusinessLogic();

console.log("");

console.log("Client: Strategy is set to reverse sorting.");
context.setStrategy(new ConcreteStrategyB());
context.doSomeBusinessLogic();
```

----------------

## Singleton Pattern
The Singleton pattern is a software design pattern that restricts the instantiation of a class to a single instance and provides a global point of access to that instance.

### Advantages
- Ensures that only one instance of the class is created, which can be useful for managing resources that need to be shared across an application.
- Provides a single point of access to the instance, making it easy to use and reducing the risk of errors that can occur when multiple instances of a class are created.
- Can improve performance by reducing the overhead associated with creating and destroying objects.

### Disadvantages
- Can make code harder to test and maintain, as the global state can lead to unexpected interactions and dependencies between components.
- Can introduce a bottleneck if the Singleton instance is heavily used and multiple threads are trying to access it simultaneously.
- Can make it harder to extend or modify the system in the future, as the Singleton instance may be tightly coupled to other parts of the system.

### When to use it
The Singleton pattern should be used when you need to ensure that only one instance of a class is created and that it can be easily accessed by other parts of the system. It is commonly used for managing resources that need to be shared across an application, such as a database connection or a configuration object. However, it should be used with caution as it can introduce complexity and make it harder to test and maintain your code.

For example, if you have a logging class that should be shared across your application, you could use the Singleton pattern to ensure that only one instance of the logging class is created and that it is easily accessible from any part of the application. This can help to improve the consistency and reliability of your logging and reduce the risk of errors that can occur when multiple instances of the logging class are created.


```typescript
class Singleton {
  private static instance: Singleton;

  // Make the constructor private to prevent direct instantiation.
  private constructor() {}

  // Create a static method to get the singleton instance.
  public static getInstance(): Singleton {
    // Check if an instance already exists, and create one if it doesn't.
    if (!Singleton.instance) {
      Singleton.instance = new Singleton();
    }

    return Singleton.instance;
  }

  // Add some functionality to the singleton instance.
  public someMethod(): void {
    console.log("Some method of the singleton is called.");
  }
}

// Usage example
const instance1 = Singleton.getInstance();
const instance2 = Singleton.getInstance();

console.log(instance1 === instance2); // true

instance1.someMethod(); // Some method of the singleton is called.
instance2.someMethod(); // Some method of the singleton is called.
```

----

## Decorator Pattern

### Overview

The Decorator Pattern is a structural design pattern that allows behavior to be added to an individual object, either statically or dynamically, without affecting the behavior of other objects in the same class. The pattern is based on the idea of wrapping a class with another class that provides additional functionality.

### Advantages
- Enhanced flexibility: The Decorator Pattern enhances the flexibility of the code by allowing new functionality to be added dynamically to objects at runtime, without affecting other objects of the same class.
- Open-closed principle: The pattern supports the open-closed principle, which means that classes should be open for extension but closed for modification. The Decorator Pattern allows new functionality to be added to objects without modifying their source code.
- Single Responsibility Principle: The pattern adheres to the Single Responsibility Principle by separating the core responsibilities of a class from the added functionality provided by decorators.
- Simplified maintenance: The Decorator Pattern simplifies maintenance by allowing the modification of individual objects, without affecting the behavior of other objects of the same class.

### Disadvantages
- Complexity: The pattern can add complexity to the code, as it requires multiple classes to be created to implement a single feature.
- Performance overhead: The Decorator Pattern can introduce performance overhead, as it involves multiple layers of object wrapping and unwrapping.
- Difficulty in debugging: The use of decorators can make it difficult to debug code, as it is not always clear which decorator is responsible for a particular behavior.
- Order of execution: The order in which decorators are applied can affect the behavior of an object, and it can be challenging to ensure that the decorators are applied in the correct order.

### The bottom line
Overall, the Decorator Pattern is a useful tool for enhancing the flexibility and maintainability of object-oriented code. However, it should be used judiciously, as it can introduce complexity and performance overhead.


### Example
```typescript
// Define the interface that all components must implement.
interface Component {
  operation(): string;
}

// Concrete component that implements the Component interface.
class ConcreteComponent implements Component {
  operation(): string {
    return "ConcreteComponent";
  }
}

// Decorator that adds additional behavior to a component.
class Decorator implements Component {
  protected component: Component;

  constructor(component: Component) {
    this.component = component;
  }

  operation(): string {
    return this.component.operation();
  }
}

// Concrete decorator that adds additional behavior to the component.
class ConcreteDecoratorA extends Decorator {
  operation(): string {
    return `ConcreteDecoratorA(${this.component.operation()})`;
  }
}

// Another concrete decorator that adds additional behavior to the component.
class ConcreteDecoratorB extends Decorator {
  operation(): string {
    return `ConcreteDecoratorB(${this.component.operation()})`;
  }
}

// Client code that uses the components and decorators.
function clientCode(component: Component) {
  console.log(`RESULT: ${component.operation()}`);
}

// Usage example
const simple = new ConcreteComponent();
const decoratorA = new ConcreteDecoratorA(simple);
const decoratorB = new ConcreteDecoratorB(decoratorA);

clientCode(simple);
clientCode(decoratorA);
clientCode(decoratorB);
```
