### Memento Pattern Documentation

---

#### Overview

The Memento pattern is a behavioral design pattern that allows an object to capture its internal state and externalize it without violating encapsulation. This pattern enables the object to be restored to its previous state at a later time, effectively implementing undo functionality. The Memento pattern consists of three main components: the Originator, the Memento, and the Caretaker. The Originator creates and uses the Memento to capture its state, while the Caretaker stores and retrieves Mementos to manage the state of the Originator.

---

#### Key Components

1. **Originator:** Creates and uses Mementos to capture and restore its internal state. It defines methods for saving and restoring its state.

2. **Memento:** Stores the internal state of the Originator. It provides a way to retrieve the state of the Originator, but prevents any other object from accessing its state.

3. **Caretaker:** Stores and retrieves Mementos to manage the state of the Originator. It is responsible for the safekeeping of Mementos and does not modify or interpret their contents.

---

#### Example Scenario

Consider an example scenario of implementing a text editor with undo functionality using the Memento pattern. The text editor allows users to type and modify text, with the ability to undo and redo changes.

##### Step 1: Implement the Memento

```java
// Memento
public class TextMemento {
    private final String text;

    public TextMemento(String text) {
        this.text = text;
    }

    public String getText() {
        return text;
    }
}
```

##### Step 2: Implement the Originator

```java
// Originator
public class TextEditor {
    private StringBuilder text;

    public TextEditor() {
        this.text = new StringBuilder();
    }

    public void appendText(String newText) {
        text.append(newText);
    }

    public String getText() {
        return text.toString();
    }

    public TextMemento save() {
        return new TextMemento(text.toString());
    }

    public void restore(TextMemento memento) {
        text = new StringBuilder(memento.getText());
    }
}
```

##### Step 3: Implement the Caretaker

```java
// Caretaker
import java.util.Stack;

public class History {
    private final Stack<TextMemento> history;

    public History() {
        this.history = new Stack<>();
    }

    public void save(TextMemento memento) {
        history.push(memento);
    }

    public TextMemento undo() {
        if (!history.isEmpty()) {
            return history.pop();
        }
        return null;
    }
}
```

##### Step 4: Use the Memento in Client Code

```java
// Client Code
public class Main {
    public static void main(String[] args) {
        TextEditor editor = new TextEditor();
        History history = new History();

        editor.appendText("Hello, ");
        history.save(editor.save());

        editor.appendText("world!");
        history.save(editor.save());

        System.out.println("Current text: " + editor.getText());

        // Undo
        editor.restore(history.undo());
        System.out.println("Text after undo: " + editor.getText());

        // Redo
        editor.restore(history.undo());
        System.out.println("Text after redo: " + editor.getText());
    }
}
```

---

#### Summary

The Memento pattern allows an object to capture its internal state and externalize it without violating encapsulation. It enables the object to be restored to its previous state at a later time, effectively implementing undo functionality. This pattern promotes encapsulation, as the internal state of the Originator is stored in a Memento object and can only be accessed through the Originator. The Memento pattern is particularly useful when you need to implement undo functionality, checkpointing, or state serialization in an object-oriented system. It enhances maintainability and flexibility by decoupling the state storage and restoration logic from the Originator, allowing for easier extension and modification of the system.
