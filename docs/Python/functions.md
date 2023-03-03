# Functions

Python Functions is a block of statements that return the specific task.

Example: A function that checks even and odd number.

```python
def check(n):
    if n%2==0:
        return "Even"
    else:
        return "Odd"

print(check(5))
```

## Types of Function Arguments

### 1. Keyword Argument

- No need to remember the order of argument.
- Use argument name and provide in any order.

```python
>>> def fun(first, second):
...     return first+second
...
>>> fun(second="banana", first="apple")
'applebanana'
```

### 2. Default Argument

- A default argument is a parameter that assumes a default value if a value is not provided in the function call for that argument.

```python
>>> def fun(a,b=5):
...     return a+b
...
>>> fun(4)
9
```

### 3. Variable Length Arguments

```python
>>> def fun(*args, **kwargs):
...     for arg in args:
...             print(arg)
...     for key, value in kwargs.items():
...             print(f"{key} - {value}")
...
>>> fun(1,2,3, four=4, five=5)
1
2
3
four - 4
five - 5
```

### 4. Required Argument

- Required arguments are those that are required to be passed to the function at the time of function call.

```python
>>> def fun(a, b):
...     return a+b
...
>>> fun(1,2)
3
>>> fun(1)
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: fun() missing 1 required positional argument: 'b'
```
