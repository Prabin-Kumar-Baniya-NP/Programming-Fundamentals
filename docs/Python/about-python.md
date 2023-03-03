### 1. Why Python is called interpreted language ?

Python is called interpreted language because it executes the program line by line. There is no compilation while running the code.

### 2. What is type coercion and does Python support type coercion ?

Type coercion is the implicit conversion of values from one data type to another. Python doesn't support type coercion like JavaScript. So, python will throw an type-error when we implicilty convert values from one data type to other.

Python Example

```python
a = '1'
b = 2
print(a+b) # TypeError: can only concatenate str (not "int") to str
```

JavaScript Example

```javascript
let a = "1";
let b = 2;
console.log(a + b); // 12
```

### 3. Why Python is called dynamically typed language ?

Python is called strongly typed language because it doesn't support type coercion. Type checking can take place before execution (static) and during execution (dynamic). Since, python is interpreted language, so type checking take place during execution. Hence, Python is called dynamically typed language.

### 4. What is PEP 8 ?

PEP stands for Python Enhancement Proposal. PEP 8 is a document that describes guidelines and best practices while writing python code.

### 5. What are Linters ?

Linters are programs that analyze code and flag errors. They provide suggestions on how to fix the errors.

Examples: pylint, pycodestyle, flake8

### 6. What are autoformatters ?

Autoformatters are programs that refactor our code to conform with PEP 8 automatically.

Examples: autopip8, yapf, black
