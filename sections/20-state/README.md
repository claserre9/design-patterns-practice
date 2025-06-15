# State Pattern

## Overview
The State pattern allows an object to alter its behavior when its internal state changes. The object will appear to change its class.

## Detailed Explanation
State objects encapsulate state-specific behavior. The context holds a reference to a state object and delegates requests to it. When the state changes, the context switches to a different state object.

### UML Diagram
```
Context -> StateA
       -> StateB
```

### Real-world Analogy
A traffic light changes behavior (color) over time. Each color state determines what cars should do.

### Supported Principles
Adheres to **Single Responsibility** by moving state-specific logic into separate classes.

## Code Examples

### Problem Without State (Python)
```python
class Player:
    def __init__(self):
        self.state = 'standing'
    def handle(self):
        if self.state == 'standing':
            print('Standing')
        elif self.state == 'running':
            print('Running')
```

### Solution with State (Python)
```python
class State:
    def handle(self, player):
        pass

class Standing(State):
    def handle(self, player):
        print('Standing')
        player.state = Running()

class Running(State):
    def handle(self, player):
        print('Running')
        player.state = Standing()

class Player:
    def __init__(self):
        self.state = Standing()
    def handle(self):
        self.state.handle(self)

player = Player()
player.handle()  # Standing
player.handle()  # Running
```

## Common Pitfalls & Warnings
1. **Too many states**: Overuse can lead to numerous small classes.
2. **Tight coupling**: Context may depend heavily on specific state implementations.

## Best Practices
- Use when an object's behavior depends on its state.
- Consider enum-based states for simple scenarios.

## Mini Exercise
Create a network connection class that transitions between `Disconnected`, `Connecting`, and `Connected` states, printing messages for each transition.
