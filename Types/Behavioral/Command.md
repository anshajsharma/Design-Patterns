### Command Pattern Documentation

---

#### Overview

The Command pattern is a behavioral design pattern that encapsulates a request as an object, thereby allowing parameterization of clients with queues, requests, and operations. It decouples the sender and receiver of a command by encapsulating the request as an object. This pattern enables the requester to be decoupled from the object that performs the action, allowing for easier parameterization of clients and providing support for undoable operations, redoable operations, and logging.

---

#### Key Components

1. **Command:** Declares an interface for executing an operation.

2. **Concrete Command:** Implements the Command interface and defines a binding between a receiver object and an action.

3. **Invoker:** Asks the command to carry out the request.

4. **Receiver:** Knows how to perform the operations associated with carrying out a request.

5. **Client:** Creates a Concrete Command object and sets its receiver.

---

#### Example Scenario

Consider an example scenario of implementing a remote control system using the Command pattern, where the remote control buttons (e.g., On, Off, Undo) are represented as commands that control different devices.

##### Step 1: Implement the Command Interface

```java
// Command Interface
public interface Command {
    void execute();
}
```

##### Step 2: Implement the Concrete Commands

```java
// Concrete Command for turning a device on
public class TurnOnCommand implements Command {
    private Device device;

    public TurnOnCommand(Device device) {
        this.device = device;
    }

    @Override
    public void execute() {
        device.turnOn();
    }
}

// Concrete Command for turning a device off
public class TurnOffCommand implements Command {
    private Device device;

    public TurnOffCommand(Device device) {
        this.device = device;
    }

    @Override
    public void execute() {
        device.turnOff();
    }
}
```

##### Step 3: Implement the Receiver

```java
// Receiver
public class Device {
    private String name;

    public Device(String name) {
        this.name = name;
    }

    public void turnOn() {
        System.out.println(name + " is turned on");
    }

    public void turnOff() {
        System.out.println(name + " is turned off");
    }
}
```

##### Step 4: Implement the Invoker

```java
// Invoker
public class RemoteControl {
    private Command command;

    public void setCommand(Command command) {
        this.command = command;
    }

    public void pressButton() {
        command.execute();
    }
}
```

##### Step 5: Use the Command Pattern in Client Code

```java
// Client Code
public class Main {
    public static void main(String[] args) {
        // Create receiver
        Device tv = new Device("TV");

        // Create commands
        Command turnOnCommand = new TurnOnCommand(tv);
        Command turnOffCommand = new TurnOffCommand(tv);

        // Create invoker
        RemoteControl remoteControl = new RemoteControl();

        // Set commands to invoker and press buttons
        remoteControl.setCommand(turnOnCommand);
        remoteControl.pressButton(); // Turns TV on

        remoteControl.setCommand(turnOffCommand);
        remoteControl.pressButton(); // Turns TV off
    }
}
```

---

#### Summary

The Command pattern encapsulates a request as an object, thereby allowing parameterization of clients with queues, requests, and operations. It decouples the sender and receiver of a command by encapsulating the request as an object. This pattern enables the requester to be decoupled from the object that performs the action, allowing for easier parameterization of clients and providing support for undoable operations, redoable operations, and logging. The Command pattern promotes flexibility, extensibility, and maintainability by providing a way to encapsulate a request as an object and parameterize clients with different requests, enabling them to be queued, logged, or undone/redone as necessary.
