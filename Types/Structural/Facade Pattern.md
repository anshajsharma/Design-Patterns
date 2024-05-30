### Facade Pattern Documentation

---

#### Overview

The Facade pattern is a structural design pattern that provides a simplified interface to a complex system of classes, interfaces, or subsystems. It hides the complexities of the system and provides a single unified interface for clients to interact with. This pattern is useful when you need to provide a simple and unified interface to a complex system or when you want to decouple clients from the implementation details of the subsystems.

---

#### Key Components

1. **Facade:** Provides a unified interface to a set of interfaces in a subsystem. It simplifies the interaction with the subsystem by providing a high-level interface that hides the complexities of the subsystem.

2. **Subsystem Classes:** Represents the individual classes or components that make up the subsystem. These classes handle the actual work of the subsystem but are hidden from clients by the facade.

---

#### Example Scenario

Consider an example scenario of using a Facade to simplify the process of booking a vacation package, which involves interacting with multiple subsystems such as flights, hotels, and car rentals.

##### Step 1: Implement the Facade

```java
// Facade
public class VacationPackageFacade {
    private FlightBookingSystem flightBookingSystem;
    private HotelBookingSystem hotelBookingSystem;
    private CarRentalSystem carRentalSystem;

    public VacationPackageFacade() {
        flightBookingSystem = new FlightBookingSystem();
        hotelBookingSystem = new HotelBookingSystem();
        carRentalSystem = new CarRentalSystem();
    }

    public void bookVacationPackage(String destination, String departureDate, int duration) {
        // Simplify the process by hiding the complexities of interacting with subsystems
        flightBookingSystem.bookFlight(destination, departureDate);
        hotelBookingSystem.bookHotel(destination, departureDate, duration);
        carRentalSystem.rentCar(destination, departureDate, duration);
    }
}
```

##### Step 2: Implement the Subsystem Classes

```java
// Subsystem Classes
public class FlightBookingSystem {
    public void bookFlight(String destination, String departureDate) {
        System.out.println("Booking flight to " + destination + " on " + departureDate);
    }
}

public class HotelBookingSystem {
    public void bookHotel(String destination, String departureDate, int duration) {
        System.out.println("Booking hotel in " + destination + " from " + departureDate + " for " + duration + " days");
    }
}

public class CarRentalSystem {
    public void rentCar(String destination, String departureDate, int duration) {
        System.out.println("Renting car in " + destination + " from " + departureDate + " for " + duration + " days");
    }
}
```

##### Step 3: Use the Facade in Client Code

```java
// Client Code
public class Main {
    public static void main(String[] args) {
        VacationPackageFacade vacationPackageFacade = new VacationPackageFacade();
        vacationPackageFacade.bookVacationPackage("Paris", "2024-07-15", 7);
    }
}
```

---

#### Summary

The Facade pattern provides a simplified interface to a complex system of classes, interfaces, or subsystems. It hides the complexities of the system and provides a single unified interface for clients to interact with. This pattern promotes encapsulation, decoupling, and simplicity by providing a high-level interface that hides the details of the subsystem from clients. The Facade pattern enhances maintainability and scalability by reducing dependencies between clients and subsystems and by providing a clear separation of concerns.
