# Decorator Pattern

## Overview
The Decorator pattern attaches additional responsibilities to an object dynamically. It provides a flexible alternative to subclassing for extending functionality.

## Detailed Explanation
A decorator wraps another object of the same interface and adds behavior before or after delegating operations. Multiple decorators can be stacked to combine behaviors without creating an explosion of subclasses.

### UML Diagram
```
Component <- Decorator
    ^          ^
Concrete   ConcreteDecorator
```

### Real-world Analogy
Coffee shop orders: you start with a plain coffee (component) and add milk or sugar decorators to extend its flavor.

### Supported Principles
Adheres to the **Open/Closed Principle**—you can add new decorators without modifying existing code.

## Code Examples

### Problem Without Decorator (Python)
```python
class Notifier:
    def send(self, message):
        print(f"Sending: {message}")

class SMSNotifier(Notifier):
    def send(self, message):
        super().send(message)
        print("via SMS")

class EmailSMSNotifier(SMSNotifier):
    def send(self, message):
        super().send(message)
        print("and Email")
```

### Solution with Decorator (Python)
```python
class NotifierBase:
    def send(self, message):
        pass

class SimpleNotifier(NotifierBase):
    def send(self, message):
        print(f"Sending: {message}")

class SMSDecorator(NotifierBase):
    def __init__(self, wrap):
        self.wrap = wrap
    def send(self, message):
        self.wrap.send(message)
        print("via SMS")

class EmailDecorator(NotifierBase):
    def __init__(self, wrap):
        self.wrap = wrap
    def send(self, message):
        self.wrap.send(message)
        print("and Email")

# Stack decorators
notifier = EmailDecorator(SMSDecorator(SimpleNotifier()))
notifier.send("Hello")
```

## Common Pitfalls & Warnings
1. **Too many small classes**: Each decorator adds a new class; use judiciously.
2. **Order dependence**: Behavior may differ depending on decorator order.

## Best Practices
- Favor composition by wrapping existing objects.
- Ensure decorators adhere to the same interface as the wrapped component.

## Mini Exercise
Create a text formatter where decorators add bold and italic styles. Chain them in different orders to see the effect.
