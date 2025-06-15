# Chain of Responsibility Pattern

## Overview
The Chain of Responsibility pattern passes a request along a chain of handlers until one of them handles it. It decouples the sender of a request from its receivers.

## Detailed Explanation
Handlers are linked in a chain. Each handler decides whether to process the request or pass it to the next handler. This pattern is helpful when multiple objects may handle a request or when you want flexible order of processing.

### UML Diagram
```
Client -> Handler -> Handler -> ...
```

### Real-world Analogy
Technical support call centers escalate issues from first-level reps to specialists until the problem is resolved.

### Supported Principles
Encourages **Single Responsibility** (each handler deals with one thing) and **Open/Closed** (new handlers can be added without altering clients).

## Code Examples

### Problem Without Chain (Python)
```python
def handle_request(level, message):
    if level == 'info':
        print(message)
    elif level == 'warning':
        print('Warn:', message)
    elif level == 'error':
        print('Error:', message)
```

### Solution with Chain of Responsibility (Python)
```python
class Handler:
    def __init__(self, next_handler=None):
        self.next = next_handler
    def handle(self, level, message):
        if self.next:
            self.next.handle(level, message)

class ErrorHandler(Handler):
    def handle(self, level, message):
        if level == 'error':
            print('Error:', message)
        else:
            super().handle(level, message)

class WarningHandler(Handler):
    def handle(self, level, message):
        if level == 'warning':
            print('Warn:', message)
        else:
            super().handle(level, message)

class InfoHandler(Handler):
    def handle(self, level, message):
        if level == 'info':
            print(message)
        else:
            super().handle(level, message)

chain = InfoHandler(WarningHandler(ErrorHandler()))
chain.handle('warning', 'Low disk space')
```

## Common Pitfalls & Warnings
1. **Unhandled requests**: Ensure the chain ends with a default handler or handles all cases.
2. **Long chains**: Deep chains may impact performance and debugging.

## Best Practices
- Use when multiple objects might handle a request.
- Keep handlers focused and chain order clear.

## Mini Exercise
Create a simple approval workflow for purchase orders with three levels of managers. Each level approves orders up to a certain amount and forwards larger ones up the chain.
