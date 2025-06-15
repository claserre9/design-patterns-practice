# Prototype Pattern

## Overview
The Prototype pattern creates new objects by cloning existing instances. It solves the problem of costly or complex object creation when similar objects are required.

## Detailed Explanation
A prototype object implements a `clone` method that copies itself. Clients obtain new objects by cloning the prototype rather than instantiating classes directly. This is useful when object creation is resource-intensive or when configuration should be duplicated.

### UML Diagram
```
Prototype (clone)
 |
 +-- ConcretePrototype
```

### Real-world Analogy
Think of making cookies with a cookie cutter: you create one mold and stamp out identical cookies quickly.

### Supported Principles
Supports **Open/Closed** by enabling new prototypes without changing existing code.

## Code Examples

### Problem Without Prototype (Python)
```python
import copy
class Tree:
    def __init__(self, height, color):
        self.height = height
        self.color = color

# Manual duplication
original = Tree(10, 'green')
clone = Tree(original.height, original.color)
```

### Solution with Prototype (Python)
```python
class TreePrototype:
    def __init__(self, height, color):
        self.height = height
        self.color = color
    def clone(self):
        return copy.deepcopy(self)

original = TreePrototype(10, 'green')
clone = original.clone()
```

## Common Pitfalls & Warnings
1. **Shallow vs deep copy**: Ensure cloning handles nested objects appropriately.
2. **Mutation**: Cloned objects may still reference the same internal mutable state if copied incorrectly.

## Best Practices
- Use when object creation is expensive or when you need many similar objects.
- Provide a clear cloning interface and decide between shallow and deep copies.

## Mini Exercise
Create a prototype for shapes that supports cloning. Instantiate one shape, clone it multiple times, and modify the clones independently.
