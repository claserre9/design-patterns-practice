# Template Method Pattern

## Overview
The Template Method pattern defines the skeleton of an algorithm in an operation, deferring some steps to subclasses. It lets subclasses redefine certain steps without changing the algorithm's structure.

## Detailed Explanation
An abstract class provides a template method that outlines the steps. Some steps have default implementations or remain abstract for subclasses to implement. This pattern is useful when many classes share the same workflow but differ in specific steps.

### UML Diagram
```
AbstractClass -> template_method()
                primitive_operation()
```

### Real-world Analogy
A recipe specifies common steps for cooking a dish but allows different ingredients or cooking times.

### Supported Principles
Applies **Hollywood Principle** ("Don't call us, we'll call you") and **Open/Closed** for algorithm customization.

## Code Examples

### Problem Without Template Method (Python)
```python
class DataExporter:
    def export_csv(self, data):
        print('prepare csv')
        print('write csv')
    def export_json(self, data):
        print('prepare json')
        print('write json')
```

### Solution with Template Method (Python)
```python
class DataExporter:
    def export(self, data):
        self.prepare(data)
        self.write(data)
    def prepare(self, data):
        pass
    def write(self, data):
        pass

class CSVExporter(DataExporter):
    def prepare(self, data):
        print('prepare csv')
    def write(self, data):
        print('write csv')

class JSONExporter(DataExporter):
    def prepare(self, data):
        print('prepare json')
    def write(self, data):
        print('write json')

CSVExporter().export([])
```

## Common Pitfalls & Warnings
1. **Inflexible ordering**: The template enforces a fixed step sequence; avoid if order must vary.
2. **Fragile base class**: Changes in the base algorithm may affect all subclasses.

## Best Practices
- Keep template methods small and focused.
- Provide hooks (optional methods) for subclasses to override if needed.

## Mini Exercise
Create an abstract game class with a `play()` template method that sets up the game, plays turns, and declares a winner. Implement a simple card game subclass.
