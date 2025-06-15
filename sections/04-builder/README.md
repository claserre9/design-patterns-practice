# Builder Pattern

## Overview
The Builder pattern separates the construction of a complex object from its representation so the same construction process can create different representations. It addresses the problem of creating objects that require many steps or optional parameters.

## Detailed Explanation
A Builder provides step-by-step methods to assemble parts of a product. A Director can orchestrate the construction, ensuring a specific order. Use this pattern when object creation involves many configurable options or when you want immutable objects assembled gradually.

### UML Diagram
```
Director -> Builder
          -> ConcreteBuilder
Product
```

### Real-world Analogy
Ordering a custom sandwich: you choose bread, fillings, and sauces step by step, then the server assembles it.

### Supported Principles
Promotes **Single Responsibility** by separating object construction logic from the representation.

## Code Examples

### Problem Without Builder (Python)
```python
class House:
    def __init__(self, floors=1, rooms=1, has_garage=False):
        self.floors = floors
        self.rooms = rooms
        self.has_garage = has_garage

# Constructor with many optional params becomes unwieldy
house = House(2, 3, True)
```

### Solution with Builder (Python)
```python
class HouseBuilder:
    def __init__(self):
        self.house = House()
    def add_floor(self):
        self.house.floors += 1
        return self
    def add_room(self):
        self.house.rooms += 1
        return self
    def add_garage(self):
        self.house.has_garage = True
        return self
    def build(self):
        return self.house

# Usage
builder = HouseBuilder()
house = (builder.add_floor()
               .add_room()
               .add_garage()
               .build())
```

## Common Pitfalls & Warnings
1. **Overkill**: Unnecessary for simple objects with few fields.
2. **State leakage**: Reusing the same builder instance without resetting can lead to unexpected results.

## Best Practices
- Use for complex objects requiring multiple construction steps.
- Keep builders stateless or provide a clear `reset` method to reuse them safely.

## Mini Exercise
Implement a pizza builder that allows chaining ingredients like sauce, cheese, and toppings. Ensure the `build()` method returns an immutable pizza object.
