## Exception Handling : Try-except-else-finally

- Try is the keyword which is used to keep the code segment under check
- Except- segment used to handle the exceptions after catching it
- Else- runs this when no exception exists
- Finally- this segment of code is always executed though there is exceptions or not

### Example 1

```python
try:
    print(2 / 0)
except NameError:
    print("The given Variable is not defined")
except ZeroDivisionError:
    print("Zero Division Error")
except:
    print(
        "Something gonna wrong"
    )  # This line is executed if some other exceptions are encountered.
else:
    print("Runs when no exception are found")
finally:
    print("Exception handling")
```
```
Output:
Zero Division Error
Exception handling
```
### Example 2

```python
try:
    print(2 / 0)
    print(q)
except ZeroDivisionError:
    print(2 / 2)
except NameError:
    print("Variable is not defined")  # This is not executed
else:
    print(100 / 10)
finally:
    print(500 / 5)
```
```
Output:
Variable is not defined
100.0
```