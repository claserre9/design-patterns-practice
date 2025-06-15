# Adapter Pattern

## Overview
The Adapter pattern converts the interface of a class into another interface clients expect. It solves the problem of incompatible interfaces so that classes can work together.

## Detailed Explanation
An adapter wraps an existing class and maps its methods to the expected interface. This pattern is useful when integrating legacy components or third-party libraries that do not match your current design.

### UML Diagram
```
Client -> Target
          ^
          |
      Adapter -> Adaptee
```

### Real-world Analogy
A power plug adapter allows devices from one country to fit sockets in another.

### Supported Principles
Encourages **Open/Closed** by allowing you to add new adapters without modifying existing code.

## Code Examples

### Problem Without Adapter (Python)
```python
class FrenchSpeaker:
    def bonjour(self):
        print("Bonjour!")

class EnglishGreeting:
    def hello(self):
        print("Hello!")

# Client expects hello() but gets bonjour()
french = FrenchSpeaker()
# french.hello()  # AttributeError
```

### Solution with Adapter (Python)
```python
class FrenchAdapter:
    def __init__(self, adaptee):
        self.adaptee = adaptee
    def hello(self):
        self.adaptee.bonjour()

french = FrenchSpeaker()
adapted = FrenchAdapter(french)
adapted.hello()  # outputs Bonjour!
```

## Common Pitfalls & Warnings
1. **Over-adapting**: Creating too many adapters can lead to unnecessary complexity.
2. **Performance**: Extra layers may introduce slight overhead; keep adapters lightweight.

## Best Practices
- Use when integrating incompatible components.
- Prefer composition over inheritance when implementing adapters.

## Mini Exercise
Wrap a third-party payment API that uses `pay(amount)` so your application can call `process_payment(amount)` instead.
