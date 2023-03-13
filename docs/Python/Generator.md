# Generator

- In Python, a generator is a special type of function that allows you to generate a sequence of values on-the-fly, without storing them in memory.

- A generator function uses the yield keyword instead of return to return a value. When a generator function is called, it returns a generator object, which is an iterator that can be used to generate the sequence of values.

```python
def my_generator():
    yield 1
    yield 2
    yield 3

gen = my_generator()

print(next(gen)) # Output: 1
print(next(gen)) # Output: 2
print(next(gen)) # Output: 3
```

- In this example, my_generator is a generator function that yields the values 1, 2, and 3. When the function is called, it returns a generator object (gen), which is used to generate the sequence of values using the next function.

- Each time next is called on the generator object, the generator function resumes execution from where it left off, and returns the next value in the sequence. When there are no more values to generate, the generator function raises a StopIteration exception to signal the end of the sequence.

- Generators are useful for generating large or infinite sequences of values, because they only generate each value as it is needed, rather than storing them all in memory at once. This makes generators memory-efficient and allows them to handle very large or infinite sequences.
