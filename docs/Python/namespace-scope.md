### 1. What is namespace in Python?

Namespace is a name given to an object. In python, there are 4 types of namespace.

a. <b>Built-in</b>:
It contains names of all of the Python built-in objects. Example: del, len, ArithemticError, IndentationError etc

b. <b>Global</b>:
The global namespace contains any names defined at the level of the main program.

c. <b>Enclosing</b>:
The namespaces created for a function which is enclosed in another function. In this example, python will create namespace for g() enclosed inside f().

```python
def f():
    def g():
        pass

    g()
```

d. <b>Local</b>:
The namespace created for a function which is local and accessible in that function.

```python
def f():
    pass
```

### 2. Explain the scope in Python.

Whenever we refer any name in Python, if it exists in multiple namespaces, the Python will follow this order.

1. Local: If you refer to x inside a function, then the interpreter first searches for it in the innermost scope that’s local to that function.

2. Enclosing: If x isn’t in the local scope but appears in a function that resides inside another function, then the interpreter searches in the enclosing function’s scope.

3. Global: If neither of the above searches is fruitful, then the interpreter looks in the global scope next.

4. Built-in: If it can’t find x anywhere else, then the interpreter tries the built-in scope.

Example 1:

```python
a = [100,200]
print(len(a))
```

On executing above code, we will get 2 as an output. Because python searches for len in built-in namespace.

Example 2:

```python
def myfun():
    a = [100, 200]
    def len(l):
        return l[0]
    return len(a)

myfun()
```

On executing above code, we will get 100 as an output. Becase Python will first search for len in local namespace. Since, we have defined len in local namespace, so python will refer to len of local namespace.

### 3. Differentiate between locals and globals in Python.

globals() returns a reference to the current global namespace dictionary.

locals() returns a copy of local namespace dictionary.

### 4. Explain about global keyword in Python.

global keyword is used to reference a name in global namespace.

```python
x = 10

def fun():
    global x
    x = 100

print(x)
```
