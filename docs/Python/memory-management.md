### 1. Discuss about memory management in Python.

In python, there is Python memory manager. It allocates memory in the private heap space. So, all python objects are stored in private heap space.

Python uses CPython interpreter. When we create an object in python, CPython creates PyObject. Every PyObject have : type, reference-count and value. Python Garbage Collector looks reference count value of every object in the heap memory and whenever any python object is not referenced (ref_count = 0), it deallocates memory of that object and free up space in the heap memeory.

### 2. How to increase the reference count of object in Python ?

Approach 1: In this example, a and b both points to same object in the heap memory.

```python
a = 1
b = 1
print(id(a) == id(b)) # True
```

Approach 2: In this example, l[0] and l[1] both points to same object in heap memory.

```python
l = [2,2]
print(id(l[0] == id(l[1]))) # True
```

### 3. How to decrease the reference count of object in Python ?

Approach 1: Del keyword removes the name as a reference to the object and decreases the reference count of object by 1.

```python
a = 10
b = 10
del a
```

Approach 2: Using None value

```python
a = 1
b = 1
print(id(a) == id(b)) # True
b = None
print(id(a) == id(b)) # False
```

Approach 3: Going out of Scope

```python
def fun():
    x = 1 # ref count of obj 1 is 1
print(x) # x is not defined, ref count of obj 1 is 0
```
