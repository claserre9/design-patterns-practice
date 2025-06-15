# Visitor Pattern

## Overview
The Visitor pattern separates an algorithm from the object structure it operates on. It lets you add new operations without modifying the objects.

## Detailed Explanation
Objects (elements) accept a visitor object that performs operations on them. Each element implements an `accept` method that calls the visitor's method. Visitors can implement operations across unrelated element classes without changing their code.

### UML Diagram
```
Visitor -> visit(ElementA)
        -> visit(ElementB)
ElementA -> accept(Visitor)
```

### Real-world Analogy
A tax auditor (visitor) can inspect different types of financial documents without altering the documents themselves.

### Supported Principles
Promotes **Open/Closed** by allowing new operations via visitors and respects **Single Responsibility**.

## Code Examples

### Problem Without Visitor (Python)
```python
class Circle:
    def draw(self):
        print('draw circle')
class Square:
    def draw(self):
        print('draw square')

shapes = [Circle(), Square()]
for s in shapes:
    s.draw()
```

### Solution with Visitor (Python)
```python
class Visitor:
    def visit_circle(self, circle):
        pass
    def visit_square(self, square):
        pass

class Shape:
    def accept(self, visitor: Visitor):
        pass

class Circle(Shape):
    def accept(self, visitor):
        visitor.visit_circle(self)
    def area(self):
        return 3.14 * 1 * 1

class Square(Shape):
    def accept(self, visitor):
        visitor.visit_square(self)
    def area(self):
        return 1 * 1

class AreaVisitor(Visitor):
    def visit_circle(self, circle):
        print('circle area', circle.area())
    def visit_square(self, square):
        print('square area', square.area())

shapes = [Circle(), Square()]
visitor = AreaVisitor()
for s in shapes:
    s.accept(visitor)
```

## Common Pitfalls & Warnings
1. **Explosion of visit methods**: Each visitor must implement methods for every element type.
2. **Element modifications**: Elements must expose an `accept` method, which can be intrusive.

## Best Practices
- Use when you need to perform unrelated operations on a set of objects.
- Keep the visitor interface stable and minimize the number of element types if possible.

## Mini Exercise
Create a visitor that serializes different shapes (circle, square) to JSON without modifying the shape classes.
