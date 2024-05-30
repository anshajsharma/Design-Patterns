Let's go through each SOLID principle with a detailed example in Java.

### 1. Single Responsibility Principle (SRP)
**Definition:** A class should have only one reason to change, meaning it should have only one job or responsibility.

**Example:**

Suppose we have a `User` class that handles both user data and persistence.

```java
public class User {
    private String username;
    private String password;

    // Constructor, getters, and setters...

    public void save() {
        // Save user to the database
    }

    public boolean validatePassword() {
        // Validate user password
    }
}
```

To adhere to SRP, we should separate these responsibilities into different classes.

```java
public class User {
    private String username;
    private String password;

    // Constructor, getters, and setters...
}

public class UserRepository {
    public void save(User user) {
        // Save user to the database
    }
}

public class UserValidator {
    public boolean validatePassword(User user) {
        // Validate user password
    }
}
```

### 2. Open/Closed Principle (OCP)
**Definition:** Software entities should be open for extension but closed for modification.

**Example:**

Suppose we have a `Shape` class and want to calculate the area of different shapes.

```java
public class AreaCalculator {
    public double calculateArea(Object shape) {
        if (shape instanceof Circle) {
            Circle circle = (Circle) shape;
            return Math.PI * circle.getRadius() * circle.getRadius();
        } else if (shape instanceof Rectangle) {
            Rectangle rectangle = (Rectangle) shape;
            return rectangle.getLength() * rectangle.getBreadth();
        }
        return 0;
    }
}
```

This violates OCP because adding a new shape requires modifying `AreaCalculator`. Instead, we should use polymorphism.

```java
public interface Shape {
    double calculateArea();
}

public class Circle implements Shape {
    private double radius;

    public Circle(double radius) {
        this.radius = radius;
    }

    public double getRadius() {
        return radius;
    }

    @Override
    public double calculateArea() {
        return Math.PI * radius * radius;
    }
}

public class Rectangle implements Shape {
    private double length;
    private double breadth;

    public Rectangle(double length, double breadth) {
        this.length = length;
        this.breadth = breadth;
    }

    @Override
    public double calculateArea() {
        return length * breadth;
    }
}

public class AreaCalculator {
    public double calculateArea(Shape shape) {
        return shape.calculateArea();
    }
}
```

### 3. Liskov Substitution Principle (LSP)
**Definition:** Objects of a superclass should be replaceable with objects of a subclass without affecting the correctness of the program.

**Example:**

Consider a `Bird` class and a `Penguin` subclass.

```java
public class Bird {
    public void fly() {
        System.out.println("Flying");
    }
}

public class Penguin extends Bird {
    @Override
    public void fly() {
        throw new UnsupportedOperationException("Penguins can't fly");
    }
}
```

This violates LSP because `Penguin` cannot be used in place of `Bird`. Instead, we should reconsider the design.

```java
public abstract class Bird {
    public abstract void move();
}

public class FlyingBird extends Bird {
    @Override
    public void move() {
        System.out.println("Flying");
    }
}

public class Penguin extends Bird {
    @Override
    public void move() {
        System.out.println("Swimming");
    }
}
```

### 4. Interface Segregation Principle (ISP)
**Definition:** Clients should not be forced to depend on interfaces they do not use.

**Example:**

Consider an `Animal` interface with several methods.

```java
public interface Animal {
    void eat();
    void fly();
    void swim();
}
```

This forces all implementations to provide all methods, even if some don't make sense. Instead, create smaller, specific interfaces.

```java
public interface Eater {
    void eat();
}

public interface Flyer {
    void fly();
}

public interface Swimmer {
    void swim();
}

public class Dog implements Eater, Swimmer {
    @Override
    public void eat() {
        System.out.println("Dog is eating");
    }

    @Override
    public void swim() {
        System.out.println("Dog is swimming");
    }
}

public class Bird implements Eater, Flyer {
    @Override
    public void eat() {
        System.out.println("Bird is eating");
    }

    @Override
    public void fly() {
        System.out.println("Bird is flying");
    }
}
```

### 5. Dependency Inversion Principle (DIP)
**Definition:** High-level modules should not depend on low-level modules. Both should depend on abstractions.

**Example:**

Consider a `UserService` that depends directly on `UserRepository`.

```java
public class UserRepository {
    public void save(User user) {
        // Save user to the database
    }
}

public class UserService {
    private UserRepository userRepository;

    public UserService() {
        this.userRepository = new UserRepository();
    }

    public void saveUser(User user) {
        userRepository.save(user);
    }
}
```

This makes `UserService` dependent on `UserRepository`. Instead, depend on an abstraction.

```java
public interface UserRepository {
    void save(User user);
}

public class UserRepositoryImpl implements UserRepository {
    @Override
    public void save(User user) {
        // Save user to the database
    }
}

public class UserService {
    private UserRepository userRepository;

    public UserService(UserRepository userRepository) {
        this.userRepository = userRepository;
    }

    public void saveUser(User user) {
        userRepository.save(user);
    }
}

// Usage
public class Main {
    public static void main(String[] args) {
        UserRepository userRepository = new UserRepositoryImpl();
        UserService userService = new UserService(userRepository);
        userService.saveUser(new User());
    }
}
```

These examples illustrate how adhering to SOLID principles can lead to more modular, maintainable, and flexible code. Let me know if you have any questions or need further elaboration on any of these principles!
