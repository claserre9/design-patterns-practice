# Abstract Factory Pattern

## Overview
The Abstract Factory pattern provides an interface for creating families of related objects without specifying their concrete classes. It solves the problem of creating cross-compatible products across multiple variants or platforms.

## Detailed Explanation
An abstract factory defines methods to create abstract product types. Concrete factories implement these methods to produce specific product variants. Client code uses the factory interface, ensuring it works with any concrete factory that adheres to the same set of products.

Use this pattern when your system must be independent of how its products are created and when you need to ensure that related products are used together.

### UML Diagram
```
AbstractFactory
+ createA()
+ createB()
|
+---- ConcreteFactory1
+---- ConcreteFactory2
```

### Real-world Analogy
Think of a furniture company that offers modern and Victorian collections. Each collection has its own style of chairs and sofas, but the client should be able to use one consistent style.

### Supported Principles
Encourages the **Open/Closed Principle** and promotes **Dependency Inversion** by depending on abstractions rather than concrete classes.

## Code Examples

### Problem Without Abstract Factory (Python)
```python
class WinButton: ...
class MacButton: ...
class WinCheckbox: ...
class MacCheckbox: ...

# Client code must choose compatible components manually
btn = WinButton()
chk = MacCheckbox()  # Incompatible
```

### Solution with Abstract Factory (Python)
```python
class GUIFactory:
    def create_button(self):
        pass
    def create_checkbox(self):
        pass

class WinFactory(GUIFactory):
    def create_button(self):
        return WinButton()
    def create_checkbox(self):
        return WinCheckbox()

class MacFactory(GUIFactory):
    def create_button(self):
        return MacButton()
    def create_checkbox(self):
        return MacCheckbox()

# Client chooses the factory, not concrete classes
factory = WinFactory()
button = factory.create_button()
checkbox = factory.create_checkbox()
```

## Common Pitfalls & Warnings
1. **Complexity**: Adding new product families requires creating new factories and product classes, which can get verbose.
2. **Rigidness**: Hard to support mixing products from different families without breaking the pattern.

## Best Practices
- Use when products must match each other (e.g., GUI kits).
- Combine with Factory Method to handle varying product implementations.

## Mini Exercise
Create an Abstract Factory for themed widgets (dark and light modes) that produces buttons and sliders. Demonstrate switching themes by changing the factory.
