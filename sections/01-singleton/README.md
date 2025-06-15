# Singleton Pattern

## Overview
The Singleton pattern ensures a class has only one instance and provides a global point of access to it. This is useful when exactly one object is needed to coordinate actions across the system, such as a configuration manager or connection pool. It solves the problem of multiple instances conflicting with each other or consuming unnecessary resources.

## Detailed Explanation
The pattern works by making a class responsible for creating and keeping its sole instance. The class hides its constructor and exposes a static method (like `get_instance()`) that returns the same instance every time. Singleton is handy when you need centralized control or shared state.

Use it when you want a single instance to manage shared resources (logging, settings) or to coordinate actions. Beware of overusing Singleton as it can introduce global state and hinder testing.

### UML Diagram
```
+--------------+
|   Singleton  |
|--------------|
| -instance    |
| +get_instance()|
+--------------+
```

### Real-world Analogy
Think of a government issuing a unique passport number – there should be only one authority that grants and stores it.

### Supported Principles
Singleton can help enforce the **Single Responsibility Principle** by centralizing shared resource management.

## Code Examples

### Problem Without Singleton (Python)
```python
class Config:
    def __init__(self):
        self.settings = {}

# Multiple instances cause inconsistency
config_a = Config()
config_b = Config()
config_a.settings['debug'] = True
print(config_b.settings)  # {}
```

### Solution With Singleton (Python)
```python
class ConfigSingleton:
    _instance = None

    def __new__(cls):
        if not cls._instance:
            cls._instance = super().__new__(cls)
            cls._instance.settings = {}
        return cls._instance

# All references point to the same instance
config_a = ConfigSingleton()
config_b = ConfigSingleton()
config_a.settings['debug'] = True
print(config_b.settings)  # {'debug': True}
```

## Common Pitfalls & Warnings
1. **Hidden dependencies**: Overusing Singleton may create tight coupling and make unit testing difficult.
2. **Concurrency issues**: In multithreaded environments, ensure thread-safe instantiation.

## Best Practices
- Use Singleton for shared, read-heavy resources like configuration or logging.
- Avoid using it as a global variable holder; consider dependency injection instead.

## Mini Exercise
Create a thread-safe Singleton logger class in Python that writes messages to a file. Ensure that multiple threads share the same logger instance.
