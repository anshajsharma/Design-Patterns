### Strategy Pattern Documentation

---

#### Overview

The Strategy pattern is a behavioral design pattern that defines a family of algorithms, encapsulates each algorithm, and makes them interchangeable. This pattern allows a client to choose from a family of algorithms at runtime without modifying the client's code. It promotes loose coupling between the client and the algorithms, enhances maintainability, and improves code reusability by separating concerns into different classes.

---

#### Key Components

1. **Context:** Maintains a reference to the chosen Strategy object and delegates the algorithm's execution to this object.

2. **Strategy:** Defines an interface or abstract class that encapsulates the algorithm's behavior.

3. **Concrete Strategy:** Implements the algorithm defined by the Strategy interface or abstract class.

---

#### Example Scenario

Consider an example scenario of implementing a payment system using the Strategy pattern. The payment system allows customers to choose from different payment methods, such as credit card, PayPal, or cash.

##### Step 1: Implement the Strategy Interface

```java
// Strategy
public interface PaymentStrategy {
    void pay(double amount);
}
```

##### Step 2: Implement the Concrete Strategies

```java
// Concrete Strategy for credit card payment
public class CreditCardPaymentStrategy implements PaymentStrategy {
    private String cardNumber;
    private String expirationDate;
    private String cvv;

    public CreditCardPaymentStrategy(String cardNumber, String expirationDate, String cvv) {
        this.cardNumber = cardNumber;
        this.expirationDate = expirationDate;
        this.cvv = cvv;
    }

    @Override
    public void pay(double amount) {
        System.out.println("Paying " + amount + " using credit card");
        // Logic for processing credit card payment
    }
}

// Concrete Strategy for PayPal payment
public class PayPalPaymentStrategy implements PaymentStrategy {
    private String email;
    private String password;

    public PayPalPaymentStrategy(String email, String password) {
        this.email = email;
        this.password = password;
    }

    @Override
    public void pay(double amount) {
        System.out.println("Paying " + amount + " using PayPal");
        // Logic for processing PayPal payment
    }
}

// Concrete Strategy for cash payment
public class CashPaymentStrategy implements PaymentStrategy {
    @Override
    public void pay(double amount) {
        System.out.println("Paying " + amount + " using cash");
        // Logic for processing cash payment
    }
}
```

##### Step 3: Implement the Context

```java
// Context
public class PaymentContext {
    private PaymentStrategy paymentStrategy;

    public PaymentContext(PaymentStrategy paymentStrategy) {
        this.paymentStrategy = paymentStrategy;
    }

    public void setPaymentStrategy(PaymentStrategy paymentStrategy) {
        this.paymentStrategy = paymentStrategy;
    }

    public void processPayment(double amount) {
        paymentStrategy.pay(amount);
    }
}
```

##### Step 4: Use the Strategy Pattern in Client Code

```java
// Client Code
public class Main {
    public static void main(String[] args) {
        PaymentContext paymentContext = new PaymentContext(new CreditCardPaymentStrategy("1234 5678 9012 3456", "12/23", "123"));

        paymentContext.processPayment(100.0);

        paymentContext.setPaymentStrategy(new PayPalPaymentStrategy("example@example.com", "password"));
        paymentContext.processPayment(50.0);

        paymentContext.setPaymentStrategy(new CashPaymentStrategy());
        paymentContext.processPayment(30.0);
    }
}
```

---

#### Summary

The Strategy pattern defines a family of algorithms, encapsulates each algorithm, and makes them interchangeable. It promotes loose coupling between clients and algorithms, enhances maintainability, and improves code reusability by separating concerns into different classes. This pattern is particularly useful when a client needs to choose from a family of algorithms at runtime or when multiple variants of an algorithm exist. The Strategy pattern is commonly used in various domains, such as payment processing, sorting algorithms, and compression algorithms.
