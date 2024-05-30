### Chain of Responsibility Pattern Documentation

---

#### Overview

The Chain of Responsibility pattern is a behavioral design pattern that allows you to pass requests along a chain of handlers. Each handler decides either to process the request or to pass it to the next handler in the chain. This pattern decouples senders and receivers of requests and allows multiple objects to handle the request without knowing the exact handler beforehand. It is useful when you have a series of processing steps for a request and want to dynamically determine which object will handle the request at runtime.

---

#### Key Components

1. **Handler:** Defines an interface for handling requests and optionally implements the successor link.

2. **ConcreteHandler:** Implements the Handler interface and handles requests it is responsible for. It can also pass requests to its successor.

3. **Client:** Initiates the request and passes it to the first handler in the chain.

---

#### Example Scenario

Consider an example scenario of processing expense reports using the Chain of Responsibility pattern. Each handler in the chain decides whether it can approve the expense report or should pass it to the next handler.

##### Step 1: Implement the Handler Interface

```java
// Handler Interface
public interface ExpenseHandler {
    void handleExpense(ExpenseReport expense);
    void setNextHandler(ExpenseHandler nextHandler);
}
```

##### Step 2: Implement the ConcreteHandlers

```java
// ConcreteHandler
public class Manager implements ExpenseHandler {
    private ExpenseHandler nextHandler;

    @Override
    public void handleExpense(ExpenseReport expense) {
        if (expense.getAmount() <= 1000) {
            System.out.println("Manager approved expense: " + expense.getAmount());
        } else if (nextHandler != null) {
            nextHandler.handleExpense(expense);
        }
    }

    @Override
    public void setNextHandler(ExpenseHandler nextHandler) {
        this.nextHandler = nextHandler;
    }
}

// Another ConcreteHandler
public class Director implements ExpenseHandler {
    private ExpenseHandler nextHandler;

    @Override
    public void handleExpense(ExpenseReport expense) {
        if (expense.getAmount() <= 5000) {
            System.out.println("Director approved expense: " + expense.getAmount());
        } else if (nextHandler != null) {
            nextHandler.handleExpense(expense);
        }
    }

    @Override
    public void setNextHandler(ExpenseHandler nextHandler) {
        this.nextHandler = nextHandler;
    }
}
```

##### Step 3: Use the Chain in Client Code

```java
// Client Code
public class Main {
    public static void main(String[] args) {
        ExpenseHandler manager = new Manager();
        ExpenseHandler director = new Director();

        manager.setNextHandler(director);

        // Create expense reports and pass them to the first handler in the chain
        manager.handleExpense(new ExpenseReport(800)); // Manager will approve
        manager.handleExpense(new ExpenseReport(3500)); // Director will approve
        manager.handleExpense(new ExpenseReport(10000)); // No one can approve
    }
}
```

---

#### Summary

The Chain of Responsibility pattern allows you to pass requests along a chain of handlers, with each handler deciding either to process the request or to pass it to the next handler in the chain. This pattern decouples senders and receivers of requests and allows multiple objects to handle the request without knowing the exact handler beforehand. It is useful when you have a series of processing steps for a request and want to dynamically determine which object will handle the request at runtime. The Chain of Responsibility pattern promotes flexibility, extensibility, and maintainability by providing a way to organize and execute a series of processing steps in a flexible and reusable manner.
