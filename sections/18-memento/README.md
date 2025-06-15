# Memento Pattern

## Overview
The Memento pattern captures and externalizes an object's internal state so that it can be restored later without violating encapsulation.

## Detailed Explanation
A memento object stores the state of the originator. Caretaker objects request mementos when they want to save state and use them to restore state when needed. This pattern is helpful for implementing undo/redo functionality.

### UML Diagram
```
Originator <-> Memento
      ^
   Caretaker
```

### Real-world Analogy
Text editors save snapshots of a document so users can revert to previous versions.

### Supported Principles
Respects **Encapsulation** by keeping the saved state private to the originator.

## Code Examples

### Problem Without Memento (Python)
```python
class Editor:
    def __init__(self):
        self.text = ''
editor = Editor()
editor.text = 'Hello'
# No easy undo mechanism
```

### Solution with Memento (Python)
```python
class EditorMemento:
    def __init__(self, text):
        self.text = text

class Editor:
    def __init__(self):
        self.text = ''
    def save(self):
        return EditorMemento(self.text)
    def restore(self, memento):
        self.text = memento.text

editor = Editor()
history = []
editor.text = 'Hello'
history.append(editor.save())
editor.text = 'Hello, World!'
editor.restore(history[-1])
print(editor.text)  # Hello
```

## Common Pitfalls & Warnings
1. **Memory usage**: Storing many mementos may consume significant memory.
2. **Exposure**: Avoid exposing the internals of the memento; keep it immutable.

## Best Practices
- Use for undo functionality or checkpoints.
- Keep mementos lightweight and encapsulated within the originator.

## Mini Exercise
Implement a game character class with position and health that can save and restore its state using the Memento pattern.
