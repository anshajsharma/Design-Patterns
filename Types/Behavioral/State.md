### State Pattern Documentation

---

#### Overview

The State pattern is a behavioral design pattern that allows an object to alter its behavior when its internal state changes. This pattern encapsulates state-dependent behavior into separate state objects and delegates the responsibility for handling state transitions to these state objects. This approach promotes loose coupling, improves readability, and simplifies maintenance by organizing the behavior of an object into a set of discrete states.

---

#### Key Components

1. **Context:** Defines the interface of interest to clients and maintains an instance of a Concrete State subclass that defines the current state.

2. **State:** Defines an interface for encapsulating the behavior associated with a particular state of the Context.

3. **Concrete State:** Implements the behavior associated with a particular state of the Context.

---

#### Example Scenario

Consider an example scenario of implementing a traffic light system using the State pattern. The traffic light can be in one of three states: Red, Yellow, or Green. Each state corresponds to a specific behavior of the traffic light.

##### Step 1: Implement the State Interface

```java
// State
public interface TrafficLightState {
    void handleRequest();
}
```

##### Step 2: Implement the Concrete States

```java
// Concrete State for the Red light state
public class RedLightState implements TrafficLightState {
    @Override
    public void handleRequest() {
        System.out.println("Switching to yellow light");
    }
}

// Concrete State for the Yellow light state
public class YellowLightState implements TrafficLightState {
    @Override
    public void handleRequest() {
        System.out.println("Switching to green light");
    }
}

// Concrete State for the Green light state
public class GreenLightState implements TrafficLightState {
    @Override
    public void handleRequest() {
        System.out.println("Switching to red light");
    }
}
```

##### Step 3: Implement the Context

```java
// Context
public class TrafficLight {
    private TrafficLightState currentState;

    public TrafficLight() {
        currentState = new RedLightState(); // Initial state is Red
    }

    public void setState(TrafficLightState state)
