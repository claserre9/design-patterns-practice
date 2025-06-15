# Observer Pattern

## Overview
The Observer pattern defines a one-to-many dependency so that when one object changes state, all its dependents are notified automatically.

## Detailed Explanation
Subjects maintain a list of observers. When the subject's state changes, it calls an update method on each observer. This pattern is handy for event-driven systems or model-view synchronization.

### UML Diagram
```
Subject -> Observer1
       -> Observer2
```

### Real-world Analogy
A newspaper subscription service notifies subscribers whenever a new issue is published.

### Supported Principles
Implements **Low Coupling** and **Dependency Inversion** by relying on a common observer interface.

## Code Examples

### Problem Without Observer (Python)
```python
class Clock:
    def tick(self):
        print('tick')

class Display:
    def show(self):
        print('show clock')

clock = Clock()
display = Display()
clock.tick()
display.show()  # Must be called manually
```

### Solution with Observer (Python)
```python
class Subject:
    def __init__(self):
        self.observers = []
    def attach(self, obs):
        self.observers.append(obs)
    def notify(self):
        for obs in self.observers:
            obs.update(self)

class Clock(Subject):
    def __init__(self):
        super().__init__()
        self.time = 0
    def tick(self):
        self.time += 1
        self.notify()

class Display:
    def update(self, subject):
        print('time', subject.time)

clock = Clock()
clock.attach(Display())
clock.tick()
```

## Common Pitfalls & Warnings
1. **Memory leaks**: Ensure observers are removed when no longer needed.
2. **Order dependency**: Observers may rely on a specific notification order.

## Best Practices
- Keep observer update methods lightweight.
- Use weak references or detach observers to avoid memory issues.

## Mini Exercise
Create a weather station subject that notifies multiple displays (temperature, humidity). Simulate data updates and show notifications.
