# Mediator Pattern

## Overview
The Mediator pattern defines an object that centralizes communication between other objects. It reduces direct dependencies between colleagues, promoting loose coupling.

## Detailed Explanation
Colleague objects send messages to the mediator instead of communicating directly with each other. The mediator routes the messages to the appropriate recipients. This is useful when you have many interacting classes, and direct references would create a tangled mess.

### UML Diagram
```
Colleague -> Mediator -> Colleague
```

### Real-world Analogy
An air traffic control tower coordinates all planes, preventing them from contacting each other directly.

### Supported Principles
Improves **Low Coupling** (GRASP) and supports **Single Responsibility** by centralizing coordination logic.

## Code Examples

### Problem Without Mediator (Python)
```python
class Button:
    def __init__(self, dialog):
        self.dialog = dialog
    def click(self):
        self.dialog.widget_changed(self)

class Dialog:
    def __init__(self):
        self.button = Button(self)
    def widget_changed(self, widget):
        print('Button clicked')
```

### Solution with Mediator (Python)
```python
class Mediator:
    def notify(self, sender, event):
        pass

class ConcreteMediator(Mediator):
    def __init__(self):
        self.button = Button(self)
        self.checkbox = Checkbox(self)
    def notify(self, sender, event):
        if sender is self.button and event == 'click':
            self.checkbox.check()

class Button:
    def __init__(self, mediator):
        self.mediator = mediator
    def click(self):
        self.mediator.notify(self, 'click')

class Checkbox:
    def __init__(self, mediator):
        self.mediator = mediator
        self.checked = False
    def check(self):
        self.checked = not self.checked
        print('Checkbox', self.checked)

ui = ConcreteMediator()
ui.button.click()
```

## Common Pitfalls & Warnings
1. **God mediator**: Mediator can become too complex if it handles too many interactions.
2. **Obscurity**: Indirect communication may make code harder to trace.

## Best Practices
- Keep mediator logic focused on coordination, not on business rules.
- Use when classes communicate in complex ways that would otherwise lead to tight coupling.

## Mini Exercise
Build a chatroom mediator where multiple user objects send messages through a central chatroom. Each user receives messages from others via the mediator.
