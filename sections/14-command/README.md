# Command Pattern

## Overview
The Command pattern encapsulates a request as an object, allowing you to parameterize clients with different requests and support undoable operations.

## Detailed Explanation
A Command object implements an interface with an `execute()` method. It stores all information required to perform an action. Invokers call `execute()` without knowing the receiver. This pattern is useful for implementing queues, logs, or undo mechanisms.

### UML Diagram
```
Client -> Invoker -> Command -> Receiver
```

### Real-world Analogy
Pressing a button on a remote control sends a command to the device; the button doesn't know the details of the action.

### Supported Principles
Promotes **Open/Closed** and **Single Responsibility** by encapsulating actions as objects.

## Code Examples

### Problem Without Command (Python)
```python
class Light:
    def turn_on(self):
        print('Light on')
    def turn_off(self):
        print('Light off')

light = Light()
# UI code directly calls methods
light.turn_on()
```

### Solution with Command (Python)
```python
class Command:
    def execute(self):
        pass

class OnCommand(Command):
    def __init__(self, light):
        self.light = light
    def execute(self):
        self.light.turn_on()

class OffCommand(Command):
    def __init__(self, light):
        self.light = light
    def execute(self):
        self.light.turn_off()

class RemoteControl:
    def __init__(self):
        self.commands = {}
    def set_command(self, name, command):
        self.commands[name] = command
    def press(self, name):
        self.commands[name].execute()

remote = RemoteControl()
remote.set_command('on', OnCommand(light))
remote.set_command('off', OffCommand(light))
remote.press('on')
```

## Common Pitfalls & Warnings
1. **Command overload**: Too many command classes can clutter code.
2. **Tight coupling**: Avoid embedding receiver logic inside commands; keep them simple.

## Best Practices
- Use for undo/redo operations or macro commands.
- Consider command queues for delayed execution.

## Mini Exercise
Implement a macro command that stores a list of commands and executes them in sequence (e.g., start coffee maker then toast bread).
