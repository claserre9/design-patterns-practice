# Proxy Pattern

## Overview
The Proxy pattern provides a surrogate or placeholder for another object to control access to it. Common uses include lazy initialization, access control, and remote proxies.

## Detailed Explanation
A proxy implements the same interface as the real subject and holds a reference to it. Calls to the proxy can perform additional logic (like access checks or caching) before delegating to the real subject.

### UML Diagram
```
Client -> Proxy -> RealSubject
```

### Real-world Analogy
A credit card acts as a proxy for cash: you use it to pay, but the real money is handled by the bank.

### Supported Principles
Promotes **Single Responsibility** by separating access logic from the real subject.

## Code Examples

### Problem Without Proxy (Python)
```python
class Image:
    def load(self):
        print("Loading heavy image")

# Client loads image even if not needed
img = Image()
img.load()
```

### Solution with Proxy (Python)
```python
class ImageInterface:
    def load(self):
        pass

class RealImage(ImageInterface):
    def load(self):
        print("Loading heavy image")

class LazyImageProxy(ImageInterface):
    def __init__(self):
        self.real_image = None
    def load(self):
        if not self.real_image:
            self.real_image = RealImage()
        self.real_image.load()

# Image is loaded only when needed
proxy = LazyImageProxy()
proxy.load()
```

## Common Pitfalls & Warnings
1. **Overhead**: Additional layers might degrade performance if used excessively.
2. **Complexity**: Keep proxy code simple to avoid confusion with the real object.

## Best Practices
- Use for lazy loading, security checks, or network proxies.
- Ensure proxy implements the same interface as the real subject for transparency.

## Mini Exercise
Write a protection proxy that checks user roles before allowing access to a secure method. Demonstrate allowed and denied access scenarios.
