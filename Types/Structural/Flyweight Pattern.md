### Flyweight Pattern Documentation

---

#### Overview

The Flyweight pattern is a structural design pattern that allows you to share objects efficiently to support large numbers of similar objects. It achieves this by storing shared state externally and passing it to the objects that require it, rather than storing it internally in each object. This pattern is useful when you need to conserve memory by sharing common state across multiple objects or when you have a large number of similar objects that can be represented more efficiently.

---

#### Key Components

1. **Flyweight:** Represents the interface for flyweight objects. It allows flyweights to receive and act on extrinsic state.

2. **Concrete Flyweight:** Implements the Flyweight interface and represents flyweight objects. It stores intrinsic state that can be shared across multiple objects.

3. **Flyweight Factory:** Manages a pool of flyweight objects and ensures that flyweights are shared efficiently. It provides methods for creating and retrieving flyweight objects.

---

#### Example Scenario

Consider an example scenario of rendering a large number of trees in a forest using the Flyweight pattern. Each tree object has intrinsic state (e.g., type, color) that can be shared among multiple trees, and extrinsic state (e.g., position) that varies for each tree.

##### Step 1: Implement the Flyweight Interface

```java
// Flyweight Interface
public interface Tree {
    void render(int x, int y);
}
```

##### Step 2: Implement the Concrete Flyweight

```java
// Concrete Flyweight
public class TreeType implements Tree {
    private final String name;
    private final String color;
    private final String texture;

    public TreeType(String name, String color, String texture) {
        this.name = name;
        this.color = color;
        this.texture = texture;
    }

    @Override
    public void render(int x, int y) {
        System.out.println("Rendering " + name + " tree at position (" + x + ", " + y + ") with color " + color + " and texture " + texture);
    }
}
```

##### Step 3: Implement the Flyweight Factory

```java
import java.util.HashMap;
import java.util.Map;

// Flyweight Factory
public class TreeFactory {
    private static final Map<String, TreeType> treeTypes = new HashMap<>();

    public static TreeType getTreeType(String name, String color, String texture) {
        String key = name + color + texture;
        if (!treeTypes.containsKey(key)) {
            treeTypes.put(key, new TreeType(name, color, texture));
        }
        return treeTypes.get(key);
    }
}
```

##### Step 4: Use the Flyweight in Client Code

```java
// Client Code
public class Main {
    public static void main(String[] args) {
        TreeType oakTree = TreeFactory.getTreeType("Oak", "Green", "Texture1");
        TreeType pineTree = TreeFactory.getTreeType("Pine", "Green", "Texture2");

        oakTree.render(10, 20);
        pineTree.render(30, 40);
    }
}
```

---

#### Summary

The Flyweight pattern allows you to share objects efficiently to support large numbers of similar objects. It achieves this by storing shared state externally and passing it to the objects that require it. This pattern promotes memory efficiency, as it reduces the amount of memory used by storing common state externally and sharing it among multiple objects. The Flyweight pattern is particularly useful when you have a large number of similar objects that can be represented more efficiently by sharing common state.
