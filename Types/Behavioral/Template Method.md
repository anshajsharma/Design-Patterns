### Template Method Pattern Documentation

---

#### Overview

The Template Method pattern is a behavioral design pattern that defines the skeleton of an algorithm in the superclass but lets subclasses override specific steps of the algorithm without changing its structure. This pattern promotes code reuse by providing a template for an algorithm and allowing subclasses to customize certain steps while keeping the overall algorithm structure intact. It is particularly useful when multiple algorithms share common behavior but differ in certain implementation details.

---

#### Key Components

1. **Abstract Class:** Defines the skeleton of an algorithm in terms of abstract methods that subclasses must implement and concrete methods that provide common behavior shared by all subclasses.

2. **Concrete Class:** Implements the abstract methods defined in the abstract class to provide concrete implementations for specific steps of the algorithm.

---

#### Example Scenario

Consider an example scenario of implementing a document converter using the Template Method pattern. The document converter converts documents of different formats (e.g., PDF, Word) to plain text format. Each document format may require different steps for conversion, but the overall structure of the conversion algorithm remains the same.

##### Step 1: Implement the Abstract Class

```java
// Abstract Class
public abstract class DocumentConverter {
    public final String convert(String document) {
        String extractedText = extractText(document);
        return postProcess(extractedText);
    }

    protected abstract String extractText(String document);

    protected String postProcess(String text) {
        // Default post-processing steps
        return text.trim(); // Trim leading and trailing whitespace
    }
}
```

##### Step 2: Implement the Concrete Classes

```java
// Concrete Class for PDF document converter
public class PdfDocumentConverter extends DocumentConverter {
    @Override
    protected String extractText(String document) {
        // Logic for extracting text from PDF document
        return "Text extracted from PDF document";
    }
}

// Concrete Class for Word document converter
public class WordDocumentConverter extends DocumentConverter {
    @Override
    protected String extractText(String document) {
        // Logic for extracting text from Word document
        return "Text extracted from Word document";
    }

    @Override
    protected String postProcess(String text) {
        // Custom post-processing for Word documents
        return text.replaceAll("\\s+", " "); // Replace multiple spaces with a single space
    }
}
```

##### Step 3: Use the Template Method Pattern

```java
// Client Code
public class Main {
    public static void main(String[] args) {
        DocumentConverter pdfConverter = new PdfDocumentConverter();
        String pdfText = pdfConverter.convert("Sample PDF document");
        System.out.println("Converted PDF text: " + pdfText);

        DocumentConverter wordConverter = new WordDocumentConverter();
        String wordText = wordConverter.convert("Sample Word document");
        System.out.println("Converted Word text: " + wordText);
    }
}
```

---

#### Summary

The Template Method pattern defines the skeleton of an algorithm in the superclass but lets subclasses override specific steps of the algorithm without changing its structure. It promotes code reuse by providing a template for an algorithm and allowing subclasses to customize certain steps while keeping the overall algorithm structure intact. This pattern is particularly useful when multiple algorithms share common behavior but differ in certain implementation details. The Template Method pattern is commonly used in various domains, such as document processing, data conversion, and workflow automation.
