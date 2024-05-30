### Factory Method Pattern (Creational)
**Purpose:** Define an interface for creating an object, but let subclasses alter the type of objects that will be created.

**When to Use:** When the exact type of object that needs to be created isn’t known until runtime, and you want to delegate the responsibility of instantiation to subclasses.

### Key Components:
1. **Product**: An interface or abstract class defining the object to be created.
2. **ConcreteProduct**: A class that implements the Product interface.
3. **Creator**: An abstract class or interface declaring the factory method.
4. **ConcreteCreator**: A class that implements the factory method to create an instance of ConcreteProduct.

### Example Implementation:
Let's consider a scenario where we have different types of animals that can be created by a factory method.

#### Step 1: Define the Product Interface
```java
// Product interface
public interface Animal {
    void speak();
}
```

#### Step 2: Create Concrete Products
```java
// Concrete Product - Dog
public class Dog implements Animal {
    @Override
    public void speak() {
        System.out.println("Woof");
    }
}

// Concrete Product - Cat
public class Cat implements Animal {
    @Override
    public void speak() {
        System.out.println("Meow");
    }
}
```

#### Step 3: Define the Creator Interface
```java
// Creator interface
public abstract class AnimalFactory {
    public abstract Animal createAnimal();
}
```

#### Step 4: Create Concrete Creators
```java
// Concrete Creator - Dog Factory
public class DogFactory extends AnimalFactory {
    @Override
    public Animal createAnimal() {
        return new Dog();
    }
}

// Concrete Creator - Cat Factory
public class CatFactory extends AnimalFactory {
    @Override
    public Animal createAnimal() {
        return new Cat();
    }
}
```

#### Step 5: Usage
```java
public class Main {
    public static void main(String[] args) {
        AnimalFactory dogFactory = new DogFactory();
        Animal dog = dogFactory.createAnimal();
        dog.speak();  // Outputs: Woof

        AnimalFactory catFactory = new CatFactory();
        Animal cat = catFactory.createAnimal();
        cat.speak();  // Outputs: Meow
    }
}
```

### Summary
The Factory Method pattern allows a class to delegate the responsibility of creating objects to its subclasses. This promotes loose coupling by eliminating the need to bind application-specific classes into the code.

### Example: More Complex Scenario
Let's consider a scenario where we need to create different types of notifications (Email, SMS) using the Factory Method pattern.

#### Step 1: Define the Product Interface
```java
// Product interface
public interface Notification {
    void notifyUser();
}
```

#### Step 2: Create Concrete Products
```java
// Concrete Product - Email Notification
public class EmailNotification implements Notification {
    @Override
    public void notifyUser() {
        System.out.println("Sending an Email notification");
    }
}

// Concrete Product - SMS Notification
public class SMSNotification implements Notification {
    @Override
    public void notifyUser() {
        System.out.println("Sending an SMS notification");
    }
}
```

#### Step 3: Define the Creator Interface
```java
// Creator interface
public abstract class NotificationFactory {
    public abstract Notification createNotification();
}
```

#### Step 4: Create Concrete Creators
```java
// Concrete Creator - Email Notification Factory
public class EmailNotificationFactory extends NotificationFactory {
    @Override
    public Notification createNotification() {
        return new EmailNotification();
    }
}

// Concrete Creator - SMS Notification Factory
public class SMSNotificationFactory extends NotificationFactory {
    @Override
    public Notification createNotification() {
        return new SMSNotification();
    }
}
```

#### Step 5: Usage
```java
public class Main {
    public static void main(String[] args) {
        NotificationFactory emailFactory = new EmailNotificationFactory();
        Notification emailNotification = emailFactory.createNotification();
        emailNotification.notifyUser();  // Outputs: Sending an Email notification

        NotificationFactory smsFactory = new SMSNotificationFactory();
        Notification smsNotification = smsFactory.createNotification();
        smsNotification.notifyUser();  // Outputs: Sending an SMS notification
    }
}
```

### Benefits of Using the Factory Method Pattern:
1. **Single Responsibility Principle**: Factory Method allows the class to delegate the responsibility of object instantiation to subclasses.
2. **Open/Closed Principle**: New product types can be added without changing the existing code.
3. **Promotes Loose Coupling**: Clients interact with interfaces rather than concrete classes, reducing dependency.

This pattern is particularly useful when the exact type of object to be created is not known until runtime, providing flexibility and extending the system easily by introducing new product types. Let me know if you need further details or another example!
