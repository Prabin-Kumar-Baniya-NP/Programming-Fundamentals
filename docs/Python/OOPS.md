# Object Oriented Programming in Python

- Class is the blueprint of object
- Object is the instance of class

```python
class Compute:
    def __init__(self, x, y, z):
        self.x = x
        self.y = y
        self.z = z

    def operation(self):
        return (self.x + self.y + self.z, self.x - self.y - self.z)


digits = Compute(3, 2, 1)
print(digits.operation())
```

## Types of Variables in Class:

1. Class(Static) Variable
2. Instance Variable

```python
class Car:
    wheel = 4  # Class(Static) Variable

    def __init__(self):
        self.company = "BMW"  # Instance Variable
        self.price = "10,00,000"  # Instance Variable
```

## Types of methods

1. Instance Method - operate on instance variables
   - Accessor Method : Used when we only need to access the value
   - Mutator Method: Used when we required to set or change the value
2. Class Method - operate on class variables
3. Static Method - doesn't depend on the state of any variable of that class.

```python
class Employee:
    dress_code = "white shirt and black pant"  # Class or Static Variable

    def __init__(self):
        self.employee_id = 0000
        self.employee_address = "0000"

    def get(self):  # Instance Method - Accessor Method
        return self.id

    def set(self, set_to):  # Instance Method - Mutator Method
        self.id = set_to

    @classmethod
    def get_dress_code(cls):  # Class method - working with class variable
        return cls.dress_code

    @staticmethod
    def random_operation():
        print("Welcome to this company")
```

## OOPS Pillar

### Abstraction

Abstraction is the process of hiding complex implementation details and providing a simple interface for the user to interact with. In Python, we can achieve abstraction by using abstract classes and interfaces.

```python
from abc import ABC, abstractmethod

class Shape(ABC):
    @abstractmethod
    def area(self):
        pass

    @abstractmethod
    def perimeter(self):
        pass

class Circle(Shape):
    def __init__(self, radius):
        self.radius = radius

    def area(self):
        return 3.14 * self.radius ** 2

    def perimeter(self):
        return 2 * 3.14 * self.radius
```

### Encapsulation

- It is the process of encapsulating the data and methods under a single unit.
- A class is an example of encapsulation as it encapsulates all the data that is member functions, variables, etc.
- <b>Protected Members</b> are those members of the class that cannot be accessed outside the class but can be accessed from within the class and its subclasses. To accomplish this in Python, just follow the convention by prefixing the name of the member by a single underscore “\_”.
- <b>Private members</b> are similar to protected members, the difference is that the class members declared private should neither be accessed outside the class nor by any base class. In Python, there is no existence of Private instance variables that cannot be accessed except inside a class. However, to define a private member prefix the member name with double underscore “\_\_”.

```python
class BankAccount:
    def __init__(self, balance):
        self.__balance = balance

    def deposit(self, amount):
        self.__balance += amount

    def withdraw(self, amount):
        if amount <= self.__balance:
            self.__balance -= amount
        else:
            print("Insufficient balance.")

    def get_balance(self):
        return self.__balance

```

- In Python, name mangling is a mechanism to avoid naming conflicts between attributes or methods of different classes. Name mangling is done by adding a double underscore (\_\_) prefix to an attribute or method name, which causes the interpreter to modify the name to avoid conflicts.

- When a name is mangled, Python renames the name by adding the class name as a prefix followed by two underscores, and then the original name. For example, if we have a class named MyClass with an attribute named **my_attribute, Python will rename the attribute to \_MyClass**my_attribute.

```python
class MyClass:
    def __init__(self):
        self.__my_attribute = 42

obj = MyClass()
print(obj.__my_attribute)  # Raises an AttributeError
print(obj._MyClass__my_attribute)  # Prints 42
```

### Polymorphism

- Polymorphism is the ability of an object to take on multiple forms.
- In Python, we can achieve polymorphism through method overloading and method overriding.
- We cannot perform method overloading in python

```python
class Animal:
    def sound(self):
        pass

class Dog(Animal):
    def sound(self):
        return "Bark"

class Cat(Animal):
    def sound(self):
        return "Meow"
```

### Inheritance

Inheritance is the process of creating new classes by inheriting attributes and methods from a parent class.

```python
class Animal:
    def __init__(self, name):
        self.name = name

    def sound(self):
        pass

class Dog(Animal):
    def sound(self):
        return "Bark"

class Cat(Animal):
    def sound(self):
        return "Meow"

dog = Dog("Fido")
print(dog.name) # Output: Fido
print(dog.sound()) # Output: Bark
```

- MRO stands for Method Resolution Order, which is the order in which Python searches for methods in a hierarchy of classes. When a method is called on an object, Python looks for the method in the class of the object, and if it's not found, it looks in the parent classes in the order specified by the MRO.

```python
class A:
    def __init__(self):
        super().__init__()
        print("A")

class B(A):
    def __init__(self):
        super().__init__()
        print("B")

class C(A):
    def __init__(self):
        super().__init__()
        print("C")

class D(B, C):
    def __init__(self):
        super().__init__()
        print("D")

obj = D() # A C B D
```

MRO for D is [D, B, C, A]

## Interview Questions

### Difference between Inheritance and Composition

- Inheritance is a mechanism where a subclass inherits the attributes and methods of its parent class. The subclass can then add or override methods and attributes as needed. Inheritance is a way to reuse code and define relationships between classes.

- Composition, on the other hand, is a mechanism where a class is built from other classes or objects. The class contains references to other objects, and it delegates some of its functionality to these objects. Composition is a way to build complex objects from simpler ones.

- Example: Creating a subclass is inheriance but building a relationship between two class A, B using one-to-one, one-to-many, many-to-one is called composition.
