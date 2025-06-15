# Bridge Pattern

## Overview
The Bridge pattern decouples an abstraction from its implementation so they can vary independently. It solves the problem of a class explosion when you need to combine multiple abstractions with multiple implementations.

## Detailed Explanation
The pattern splits a large class or set of closely related classes into two separate hierarchies: Abstraction and Implementation. The Abstraction holds a reference to an Implementation object and delegates work to it. This allows each hierarchy to evolve without affecting the other.

### UML Diagram
```
Abstraction -> Implementor
      ^            ^
   Refined     ConcreteImplementor
```

### Real-world Analogy
Think of a remote control (abstraction) that can operate different devices (TV, radio). The remote sends commands to the device without knowing its details.

### Supported Principles
Aligns with the **Open/Closed Principle** and promotes **Dependency Inversion**.

## Code Examples

### Problem Without Bridge (Python)
```python
class WindowsDarkButton: ...
class WindowsLightButton: ...
class LinuxDarkButton: ...
class LinuxLightButton: ...
# Many classes for each combination
```

### Solution with Bridge (Python)
```python
class Button:
    def __init__(self, platform_impl):
        self.platform = platform_impl
    def draw(self):
        self.platform.draw_button()

class WindowsImpl:
    def draw_button(self):
        print("Windows button")

class LinuxImpl:
    def draw_button(self):
        print("Linux button")

# Use any combination
button = Button(WindowsImpl())
button.draw()
```

## Common Pitfalls & Warnings
1. **Unnecessary abstraction**: Don't use Bridge if you only have a single implementation.
2. **Increased indirection**: Two layers may add complexity for simple scenarios.

## Best Practices
- Use when both abstraction and implementation may change independently.
- Keep interfaces minimal to avoid tight coupling between layers.

## Mini Exercise
Create a drawing app where different shapes (circle, square) use different rendering APIs (vector, raster) via the Bridge pattern. Demonstrate mixing shapes and renderers.
