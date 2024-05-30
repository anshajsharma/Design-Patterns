### Composite Pattern Documentation

---

#### Overview

The Composite pattern is a structural design pattern that allows you to compose objects into tree structures to represent part-whole hierarchies. It enables clients to treat individual objects and compositions of objects uniformly. This pattern is useful when dealing with hierarchical structures where clients need to interact with individual objects and compositions in a consistent manner.

---

#### Key Components

1. **Component:** Declares the interface for objects in the composition hierarchy.

2. **Leaf:** Represents individual objects in the composition hierarchy. Implements the Component interface.

3. **Composite:** Represents compositions of objects in the composition hierarchy. Implements the Component interface and may contain Leaf and/or other Composite objects.

---

#### Example Scenario

Consider an example scenario of representing a hierarchical structure of files and directories using the Composite pattern.

##### Step 1: Define the Component Interface

```java
// Component Interface
public interface FileSystemComponent {
    void display();
}
```

##### Step 2: Implement the Leaf

```java
// Leaf (File)
public class File implements FileSystemComponent {
    private String name;

    public File(String name) {
        this.name = name;
    }

    @Override
    public void display() {
        System.out.println("File: " + name);
    }
}
```

##### Step 3: Implement the Composite

```java
import java.util.ArrayList;
import java.util.List;

// Composite (Directory)
public class Directory implements FileSystemComponent {
    private String name;
    private List<FileSystemComponent> components;

    public Directory(String name) {
        this.name = name;
        this.components = new ArrayList<>();
    }

    public void addComponent(FileSystemComponent component) {
        components.add(component);
    }

    public void removeComponent(FileSystemComponent component) {
        components.remove(component);
    }

    @Override
    public void display() {
        System.out.println("Directory: " + name);
        for (FileSystemComponent component : components) {
            component.display();
        }
    }
}
```

##### Step 4: Use the Composite in Client Code

```java
// Client Code
public class Main {
    public static void main(String[] args) {
        // Create leaf objects
        FileSystemComponent file1 = new File("file1.txt");
        FileSystemComponent file2 = new File("file2.txt");

        // Create composite object
        Directory directory = new Directory("root");

        // Add leaf objects to composite
        directory.addComponent(file1);
        directory.addComponent(file2);

        // Display composite
        directory.display();
    }
}
```

---

#### Summary

The Composite pattern allows you to represent part-whole hierarchies as tree structures, enabling clients to treat individual objects and compositions uniformly. It simplifies the interaction with complex hierarchical structures by providing a consistent interface. This pattern promotes code reuse, flexibility, and scalability by allowing objects and compositions to be added, removed, and manipulated dynamically. The Composite pattern is particularly useful when dealing with recursive structures or when you need to represent hierarchical relationships in a clear and concise manner.
