# Facade Pattern

## Overview
The Facade pattern provides a simplified interface to a complex subsystem. It hides the intricacies of the subsystem and exposes a single entry point for clients.

## Detailed Explanation
A facade object wraps several underlying classes and delegates calls to them. Clients interact with the facade rather than multiple subsystems, reducing coupling and making the API easier to use.

### UML Diagram
```
Facade -> SubsystemA
        -> SubsystemB
```

### Real-world Analogy
A hotel concierge acts as a single point of contact for guests, handling various services (booking, information, transport) without exposing internal operations.

### Supported Principles
Improves **Law of Demeter** by limiting the knowledge clients need about the subsystem.

## Code Examples

### Problem Without Facade (Python)
```python
class CPU: ...
class Memory: ...
class Disk: ...

cpu = CPU()
mem = Memory()
mem.load()  # Many calls
```

### Solution with Facade (Python)
```python
class ComputerFacade:
    def __init__(self):
        self.cpu = CPU()
        self.mem = Memory()
        self.disk = Disk()
    def start(self):
        self.cpu.freeze()
        self.mem.load()
        self.cpu.execute()

computer = ComputerFacade()
computer.start()
```

## Common Pitfalls & Warnings
1. **Oversimplification**: Hiding too much can limit advanced use cases.
2. **God object**: Avoid turning the facade into a monolithic interface with unrelated features.

## Best Practices
- Provide a clear, minimal interface that covers common scenarios.
- Keep the facade thin; heavy logic should remain in subsystems.

## Mini Exercise
Design a facade for a multimedia library that handles loading, playing, and stopping both audio and video files.
