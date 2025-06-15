# Iterator Pattern

## Overview
The Iterator pattern provides a way to access elements of an aggregate object sequentially without exposing its underlying representation.

## Detailed Explanation
An iterator object maintains the current position during iteration. The aggregate (collection) exposes a method to create an iterator. This pattern decouples traversal logic from the collection itself.

### UML Diagram
```
Client -> Iterator -> Aggregate
```

### Real-world Analogy
A remote control that flips through TV channels without needing to know how channels are stored inside the TV.

### Supported Principles
Supports **Single Responsibility** by separating traversal from collection logic, and **Open/Closed** by allowing new iterators without modifying collections.

## Code Examples

### Problem Without Iterator (Python)
```python
numbers = [1, 2, 3]
index = 0
while index < len(numbers):
    print(numbers[index])
    index += 1
```

### Solution with Iterator (Python)
```python
class NumberCollection:
    def __init__(self, numbers):
        self.numbers = numbers
    def __iter__(self):
        return NumberIterator(self.numbers)

class NumberIterator:
    def __init__(self, numbers):
        self._numbers = numbers
        self._index = 0
    def __next__(self):
        if self._index >= len(self._numbers):
            raise StopIteration
        value = self._numbers[self._index]
        self._index += 1
        return value
    def __iter__(self):
        return self

collection = NumberCollection([1, 2, 3])
for num in collection:
    print(num)
```

## Common Pitfalls & Warnings
1. **Concurrent modification**: Modifying a collection during iteration can cause errors.
2. **Stateful iterators**: Resetting the iterator may require a new object.

## Best Practices
- Keep iterators lightweight and short-lived.
- Support Python's iterator protocol (`__iter__` and `__next__` methods).

## Mini Exercise
Create an iterator for a binary tree that traverses nodes in-order. Use it to print values from a simple tree structure.
