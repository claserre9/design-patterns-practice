# Composite Pattern

## Overview
The Composite pattern composes objects into tree structures to represent part-whole hierarchies. It lets clients treat individual objects and compositions uniformly.

## Detailed Explanation
A common interface is defined for both simple (leaf) and complex (composite) objects. Composites contain children and delegate operations to them. This pattern is useful for representing hierarchies like file systems or UI components.

### UML Diagram
```
Component
  + operation()
  |
  +-- Leaf
  +-- Composite -> children[]
```

### Real-world Analogy
Folders (composites) can contain files or other folders; operations like size can be applied uniformly.

### Supported Principles
Follows the **Open/Closed** and **Liskov Substitution** principles by treating leaf and composite the same through a common interface.

## Code Examples

### Problem Without Composite (Python)
```python
class File:
    def __init__(self, name):
        self.name = name
class Folder:
    def __init__(self, name):
        self.name = name
        self.children = []

# Client must handle files and folders differently
```

### Solution with Composite (Python)
```python
class Component:
    def operation(self):
        pass

class FileLeaf(Component):
    def __init__(self, name):
        self.name = name
    def operation(self):
        print(f"File: {self.name}")

class FolderComposite(Component):
    def __init__(self, name):
        self.name = name
        self.children = []
    def add(self, child: Component):
        self.children.append(child)
    def operation(self):
        print(f"Folder: {self.name}")
        for child in self.children:
            child.operation()

# Client code
root = FolderComposite("root")
root.add(FileLeaf("file1"))
sub = FolderComposite("sub")
sub.add(FileLeaf("file2"))
root.add(sub)
root.operation()
```

## Common Pitfalls & Warnings
1. **Exposing management methods**: Keep add/remove operations on composite only if needed by clients.
2. **Performance**: Traversal of large trees can be slow if not managed carefully.

## Best Practices
- Use when you need to treat individual objects and groups the same way.
- Combine with Iterator or Visitor for complex operations over the tree.

## Mini Exercise
Create a menu system where menu items and submenus implement the same `render()` method. Build a menu tree and call `render()` on the root.
