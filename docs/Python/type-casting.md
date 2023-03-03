# Type-Casting in Python

Type Casting is the process of converting values from one data type to another data type.

There are 2 types of type-casting in python:

1. Implicit Type-Casting
2. Explicit Type-Casting

## Implicit Type-Casting

In this type of type-casting, Python converts values from one data type to another implicitly / automatically.

```python
>>> a = 1
>>> b = 2.1
>>> c = a + b
>>> c
3.1
>>> type(c)
<class 'float'>
```

## Explicit Type-Casting

In this type of type-casting, the programmer explicitly converts values from one data type to another.

Example: int to float, float to int, int to str

```python
>>> a = 1
>>> type(a)
<class 'int'>
>>> a = float(a)
>>> a
1.0
>>> type(a)
<class 'float'>
```