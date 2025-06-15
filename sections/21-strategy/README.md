# Strategy Pattern

## Overview
The Strategy pattern defines a family of algorithms, encapsulates each one, and makes them interchangeable. It lets the algorithm vary independently from clients that use it.

## Detailed Explanation
A context object holds a reference to a strategy interface. Different concrete strategies implement the interface with various algorithms. The context delegates execution to the selected strategy at runtime.

### UML Diagram
```
Context -> Strategy
          ^
      ConcreteStrategy
```

### Real-world Analogy
Sorting a list can use different strategies (quick sort, merge sort) depending on data characteristics.

### Supported Principles
Applies **Open/Closed** and **Dependency Inversion** by programming to an interface.

## Code Examples

### Problem Without Strategy (Python)
```python
def sort_numbers(nums, order='asc'):
    if order == 'asc':
        return sorted(nums)
    elif order == 'desc':
        return sorted(nums, reverse=True)
```

### Solution with Strategy (Python)
```python
class SortStrategy:
    def sort(self, data):
        pass

class AscendingStrategy(SortStrategy):
    def sort(self, data):
        return sorted(data)

class DescendingStrategy(SortStrategy):
    def sort(self, data):
        return sorted(data, reverse=True)

class SortContext:
    def __init__(self, strategy: SortStrategy):
        self.strategy = strategy
    def sort(self, data):
        return self.strategy.sort(data)

context = SortContext(AscendingStrategy())
print(context.sort([3,1,2]))
```

## Common Pitfalls & Warnings
1. **Too many strategy classes**: Create strategies only when algorithms truly vary.
2. **Context complexity**: Avoid mixing context logic with strategy selection.

## Best Practices
- Define a clear strategy interface.
- Use dependency injection to choose strategies at runtime.

## Mini Exercise
Implement a payment processor that supports multiple payment strategies (credit card, PayPal). Switch strategies during execution to process different orders.
