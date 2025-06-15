# Factory Method Pattern

## Overview
The Factory Method pattern delegates object creation to subclasses, allowing them to decide which class to instantiate. It solves the problem of creating objects without specifying the exact class in the main code, promoting flexibility and extensibility.

## Detailed Explanation
The pattern defines an interface or abstract class containing a factory method. Subclasses override this method to create specific objects. Clients use the base class reference, enabling them to interact with objects through a common interface.

Use Factory Method when a class cannot anticipate the exact class of objects it must create or when subclasses need to vary the objects they create.

### UML Diagram
```
Creator
+ factory_method()
+ operation()
|
+---- ConcreteCreator
      + factory_method()
```

### Real-world Analogy
Consider a document editor framework where each application (text editor, diagram editor) must create its own document objects, but all use a common framework.

### Supported Principles
Supports the **Open/Closed Principle** by allowing new product types through subclassing.

## Code Examples

### Problem Before Factory Method (Python)
```python
class Button:
    def click(self):
        pass

class WindowsButton(Button):
    def click(self):
        print("Windows button clicked")

class LinuxButton(Button):
    def click(self):
        print("Linux button clicked")

# Directly instantiating concrete classes
btn = WindowsButton()
btn.click()
```

### Solution with Factory Method (Python)
```python
class Dialog:
    def render(self):
        ok = self.create_button()
        ok.click()

    def create_button(self) -> Button:
        raise NotImplementedError

class WindowsDialog(Dialog):
    def create_button(self) -> Button:
        return WindowsButton()  # Concrete product

class LinuxDialog(Dialog):
    def create_button(self) -> Button:
        return LinuxButton()

# Client code
os_dialog = WindowsDialog()
os_dialog.render()
```

## Common Pitfalls & Warnings
1. **Too many subclasses**: Overuse can lead to class explosion if every variation requires a new subclass.
2. **Complex hierarchy**: Hard to maintain if factory logic becomes complicated.

## Best Practices
- Use when you expect new product variants.
- Keep the factory method simple; delegate complex logic to separate classes if needed.

## Mini Exercise
Implement a logging framework where different loggers (file, console) are created via Factory Method. Add a new logger type without modifying existing code.
