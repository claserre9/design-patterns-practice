# Flyweight Pattern

## Overview
The Flyweight pattern minimizes memory usage by sharing as much data as possible with similar objects. It solves the problem of using large numbers of fine-grained objects that share common state.

## Detailed Explanation
Flyweight objects have two types of state: intrinsic (shared) and extrinsic (context-dependent). The Flyweight factory manages a pool of shared objects, reusing them instead of creating new ones for identical data.

### UML Diagram
```
FlyweightFactory -> Flyweight (shared)
                   UnsharedFlyweight
```

### Real-world Analogy
Text editors share font metadata across thousands of characters; only character positions differ.

### Supported Principles
Follows the **Flyweight** principle from GRASP of managing shared objects. Also supports **Single Responsibility** by separating shared state.

## Code Examples

### Problem Without Flyweight (Python)
```python
class Tree:
    def __init__(self, type, color):
        self.type = type
        self.color = color

# Creating thousands of trees uses lots of memory
forest = [Tree('Oak', 'green') for _ in range(10000)]
```

### Solution with Flyweight (Python)
```python
class TreeType:
    def __init__(self, type, color):
        self.type = type
        self.color = color

class TreeFactory:
    _types = {}
    @classmethod
    def get_type(cls, type, color):
        key = (type, color)
        if key not in cls._types:
            cls._types[key] = TreeType(type, color)
        return cls._types[key]

class Tree:
    def __init__(self, tree_type, x, y):
        self.tree_type = tree_type  # shared flyweight
        self.x = x
        self.y = y

forest = [Tree(TreeFactory.get_type('Oak', 'green'), i, i) for i in range(10000)]
```

## Common Pitfalls & Warnings
1. **Premature optimization**: Only use when memory is a real concern.
2. **Complexity**: Managing extrinsic state may complicate your code.

## Best Practices
- Identify shared data that can be externalized.
- Use a factory to manage flyweights and ensure reuse.

## Mini Exercise
Implement a simple word processor character class where glyph objects are shared using Flyweight. Demonstrate memory saving by counting unique glyph instances.
