### Singleton Pattern (Creational)
**Purpose:** Ensure a class has only one instance and provide a global point of access to it.

**When to Use:** When you need exactly one instance of a class to coordinate actions across the system, such as a database connection, logging, configuration settings, or a thread pool.

#### Key Points:
1. **Private Constructor:** Prevents the instantiation of the class from other classes.
2. **Static Instance:** Holds the single instance of the class.
3. **Public Static Method:** Provides the global point of access to the instance.

#### Example Implementation:
There are several ways to implement the Singleton pattern in Java. Let's look at a few common methods.

### Basic Singleton (Lazy Initialization)
This is the simplest form where the instance is created when it is first requested.

```java
public class Singleton {
    private static Singleton instance;

    // Private constructor to prevent instantiation
    private Singleton() {
    }

    // Public method to provide access to the instance
    public static Singleton getInstance() {
        if (instance == null) {
            instance = new Singleton();
        }
        return instance;
    }
}

// Usage
public class Main {
    public static void main(String[] args) {
        Singleton s1 = Singleton.getInstance();
        Singleton s2 = Singleton.getInstance();

        System.out.println(s1 == s2);  // true, both references point to the same instance
    }
}
```

### Thread-Safe Singleton (Synchronized Method)
To make the singleton thread-safe, you can synchronize the `getInstance` method.

```java
public class Singleton {
    private static Singleton instance;

    private Singleton() {
    }

    public static synchronized Singleton getInstance() {
        if (instance == null) {
            instance = new Singleton();
        }
        return instance;
    }
}
```

### Thread-Safe Singleton (Double-Checked Locking)
This method reduces the overhead of acquiring a lock by first checking the `instance` field without synchronization.

```java
public class Singleton {
    private static volatile Singleton instance;

    private Singleton() {
    }

    public static Singleton getInstance() {
        if (instance == null) {
            synchronized (Singleton.class) {
                if (instance == null) {
                    instance = new Singleton();
                }
            }
        }
        return instance;
    }
}
```

### Eager Initialization
The instance is created at the time of class loading. This method is simple but doesn't provide the flexibility of lazy initialization.

```java
public class Singleton {
    private static final Singleton instance = new Singleton();

    private Singleton() {
    }

    public static Singleton getInstance() {
        return instance;
    }
}
```

### Bill Pugh Singleton Design
This method uses a static inner helper class to create the singleton instance. It's the most efficient way to implement a Singleton in Java.

```java
public class Singleton {
    private Singleton() {
    }

    private static class SingletonHelper {
        private static final Singleton INSTANCE = new Singleton();
    }

    public static Singleton getInstance() {
        return SingletonHelper.INSTANCE;
    }
}
```

### Enum Singleton
Using an enum is a thread-safe and straightforward way to implement a Singleton. It also protects against serialization issues and reflection attacks.

```java
public enum Singleton {
    INSTANCE;

    // Other methods can be added here
    public void someMethod() {
        // implementation
    }
}

// Usage
public class Main {
    public static void main(String[] args) {
        Singleton singleton = Singleton.INSTANCE;
        singleton.someMethod();
    }
}
```

### Summary
The Singleton pattern ensures a class has only one instance and provides a global point of access to it. The choice of implementation depends on the specific requirements of your project, such as whether thread safety is needed or if lazy initialization is preferred.

Let me know if you need further details or examples on any specific part!
