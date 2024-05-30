### Interpreter Pattern Documentation

---

#### Overview

The Interpreter pattern is a behavioral design pattern that defines a grammatical representation for a language and provides an interpreter to evaluate sentences in the language. It is used to solve problems related to defining a language, interpreting sentences in the language, and executing specific actions based on those interpretations. This pattern involves defining a grammar for the language, representing each rule of the grammar as a class, and using recursion to interpret sentences in the language.

---

#### Key Components

1. **Abstract Expression:** Declares an abstract Interpret operation that is common to all nodes in the abstract syntax tree (AST).

2. **Terminal Expression:** Implements the Interpret operation for terminal symbols in the grammar.

3. **Non-terminal Expression:** Represents complex rules in the grammar and typically consists of one or more subexpressions.

4. **Context:** Contains information that is global to the interpreter.

5. **Client:** Builds an abstract syntax tree representing a sentence in the language and invokes the Interpret operation to execute the interpretation.

---

#### Example Scenario

Consider an example scenario of implementing an interpreter for a simple arithmetic expression language that supports addition and subtraction.

##### Step 1: Implement the Abstract Expression

```java
// Abstract Expression
public interface Expression {
    int interpret(Context context);
}
```

##### Step 2: Implement the Terminal Expressions

```java
// Terminal Expression for a variable
public class VariableExpression implements Expression {
    private String variable;

    public VariableExpression(String variable) {
        this.variable = variable;
    }

    @Override
    public int interpret(Context context) {
        return context.getValue(variable);
    }
}

// Terminal Expression for a constant
public class ConstantExpression implements Expression {
    private int constant;

    public ConstantExpression(int constant) {
        this.constant = constant;
    }

    @Override
    public int interpret(Context context) {
        return constant;
    }
}
```

##### Step 3: Implement the Non-terminal Expression

```java
// Non-terminal Expression for addition
public class AddExpression implements Expression {
    private Expression left;
    private Expression right;

    public AddExpression(Expression left, Expression right) {
        this.left = left;
        this.right = right;
    }

    @Override
    public int interpret(Context context) {
        return left.interpret(context) + right.interpret(context);
    }
}

// Non-terminal Expression for subtraction
public class SubtractExpression implements Expression {
    private Expression left;
    private Expression right;

    public SubtractExpression(Expression left, Expression right) {
        this.left = left;
        this.right = right;
    }

    @Override
    public int interpret(Context context) {
        return left.interpret(context) - right.interpret(context);
    }
}
```

##### Step 4: Implement the Context

```java
// Context
public class Context {
    private Map<String, Integer> variables;

    public Context() {
        this.variables = new HashMap<>();
    }

    public void assign(String variable, int value) {
        variables.put(variable, value);
    }

    public int getValue(String variable) {
        return variables.get(variable);
    }
}
```

##### Step 5: Use the Interpreter in Client Code

```java
// Client Code
public class Main {
    public static void main(String[] args) {
        // Define variables and values
        Context context = new Context();
        context.assign("x", 10);
        context.assign("y", 5);

        // Create expressions
        Expression expression = new AddExpression(
            new VariableExpression("x"),
            new SubtractExpression(
                new ConstantExpression(20),
                new VariableExpression("y")
            )
        );

        // Interpret and print result
        int result = expression.interpret(context);
        System.out.println("Result: " + result);
    }
}
```

---

#### Summary

The Interpreter pattern defines a grammatical representation for a language and provides an interpreter to evaluate sentences in the language. It is used to solve problems related to defining a language, interpreting sentences in the language, and executing specific actions based on those interpretations. This pattern involves defining a grammar for the language, representing each rule of the grammar as a class, and using recursion to interpret sentences in the language. The Interpreter pattern promotes flexibility, extensibility, and maintainability by providing a way to interpret sentences in a language and execute specific actions based on those interpretations. It is particularly useful when dealing with problems related to defining domain-specific languages, parsing expressions, and executing specific operations based on those expressions.
