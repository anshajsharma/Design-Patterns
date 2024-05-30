### Decorator Pattern Documentation

---

#### Overview

The Decorator pattern is a structural design pattern that allows behavior to be added to individual objects dynamically, without affecting the behavior of other objects from the same class. It involves attaching new responsibilities to objects by wrapping them with one or more decorator objects. This pattern is useful when you need to extend the functionality of objects in a flexible and reusable way, without subclassing.

---

#### Key Components

1. **Component:** Defines the interface for objects that can have responsibilities added to them dynamically.

2. **Concrete Component:** Represents the basic object to which additional responsibilities can be added.

3. **Decorator:** Maintains a reference to a Component object and implements the Component interface. It also has an association with the Component interface.

4. **Concrete Decorator:** Adds new responsibilities to the Component by extending the functionality of the Decorator.

---

#### Example Scenario

Consider an example scenario of decorating a simple coffee order with additional options using the Decorator pattern.

##### Step 1: Define the Component Interface

```java
// Component Interface
public interface Coffee {
    String getDescription();
    double cost();
}
```

##### Step 2: Implement the Concrete Component

```java
// Concrete Component
public class SimpleCoffee implements Coffee {
    @Override
    public String getDescription() {
        return "Simple Coffee";
    }

    @Override
    public double cost() {
        return 1.0;
    }
}
```

##### Step 3: Implement the Decorator

```java
// Decorator
public abstract class CoffeeDecorator implements Coffee {
    protected Coffee coffee;

    public CoffeeDecorator(Coffee coffee) {
        this.coffee = coffee;
    }

    @Override
    public String getDescription() {
        return coffee.getDescription();
    }

    @Override
    public double cost() {
        return coffee.cost();
    }
}
```

##### Step 4: Implement Concrete Decorators

```java
// Concrete Decorator for Milk
public class MilkDecorator extends CoffeeDecorator {
    public MilkDecorator(Coffee coffee) {
        super(coffee);
    }

    @Override
    public String getDescription() {
        return coffee.getDescription() + ", with Milk";
    }

    @Override
    public double cost() {
        return coffee.cost() + 0.5;
    }
}

// Concrete Decorator for Sugar
public class SugarDecorator extends CoffeeDecorator {
    public SugarDecorator(Coffee coffee) {
        super(coffee);
    }

    @Override
    public String getDescription() {
        return coffee.getDescription() + ", with Sugar";
    }

    @Override
    public double cost() {
        return coffee.cost() + 0.2;
    }
}
```

##### Step 5: Use the Decorator in Client Code

```java
// Client Code
public class Main {
    public static void main(String[] args) {
        Coffee coffee = new SimpleCoffee();
        System.out.println("Description: " + coffee.getDescription() + ", Cost: $" + coffee.cost());

        // Decorate with Milk
        coffee = new MilkDecorator(coffee);
        System.out.println("Description: " + coffee.getDescription() + ", Cost: $" + coffee.cost());

        // Decorate with Sugar
        coffee = new SugarDecorator(coffee);
        System.out.println("Description: " + coffee.getDescription() + ", Cost: $" + coffee.cost());
    }
}
```

---

#### Summary

The Decorator pattern allows behavior to be added to objects dynamically by wrapping them with decorator objects. It promotes flexibility and extensibility by enabling the addition of new responsibilities to objects without modifying their structure. This pattern is particularly useful when you need to extend the functionality of objects in a flexible and reusable way, without subclassing. The Decorator pattern enhances the maintainability and scalability of the code by allowing behavior to be composed dynamically at runtime.
