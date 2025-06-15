# Interpreter Pattern

## Overview
The Interpreter pattern defines a representation of a grammar along with an interpreter that uses the representation to interpret sentences. It's used to process and evaluate language-like expressions.

## Detailed Explanation
Each grammar rule is represented by a class in an abstract syntax tree. Interpreters traverse the tree, evaluating each node. This pattern is helpful for simple languages such as arithmetic expressions or configuration DSLs.

### UML Diagram
```
Client -> AbstractExpression
            ^
      Terminal / Nonterminal
```

### Real-world Analogy
Regular expressions are parsed and interpreted according to a grammar by regex engines.

### Supported Principles
Leverages **Single Responsibility** (each expression class handles one rule) and **Open/Closed** for extending grammar.

## Code Examples

### Problem Without Interpreter (Python)
```python
expr = "1 + 2 + 3"
result = eval(expr)  # Risky and not extensible
```

### Solution with Interpreter (Python)
```python
class Number:
    def __init__(self, value):
        self.value = value
    def interpret(self):
        return self.value

class Add:
    def __init__(self, left, right):
        self.left = left
        self.right = right
    def interpret(self):
        return self.left.interpret() + self.right.interpret()

# Build AST for 1 + (2 + 3)
expression = Add(Number(1), Add(Number(2), Number(3)))
print(expression.interpret())  # 6
```

## Common Pitfalls & Warnings
1. **Complex grammars**: Interpreter works best for small languages; large grammars can become unwieldy.
2. **Performance**: Recursively interpreting may be slower than compiled solutions.

## Best Practices
- Use when the grammar is simple and stable.
- For complex languages, consider parser generators or other techniques.

## Mini Exercise
Extend the example to include subtraction and multiplication expressions. Build and interpret the expression `(4 - 2) * 3`.
