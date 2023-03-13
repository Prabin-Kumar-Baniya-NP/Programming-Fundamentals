# Decorator 

- In Python, a decorator is a design pattern that allows you to add behavior to a function or class. A decorator is a callable object that takes another function or class as an argument, modifies it, and returns it as a new function or class.

- Decorators are useful for adding functionality to existing code without modifying it. They allow you to separate concerns and keep your code modular and reusable.

### Example

```python
def my_decorator(func):
    def wrapper():
        print("Before the function is called.")
        func()
        print("After the function is called.")
    return wrapper

@my_decorator
def say_hello():
    print("Hello!")

say_hello()
```
Output
```
Before the function is called.
Hello!
After the function is called.
```