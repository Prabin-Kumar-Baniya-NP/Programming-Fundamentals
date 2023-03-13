# Type Hints and Annotation

### Variable Annotation

```python
x: int = 1
```

### Function Annotation

```python
def add(a: int, b: int) -> int:
    return a+b
```

### List Type

```python
from typing import List

x: List[List[int]] = [[1,2], [3,4]]
```

### Dictionary Type

```python
from typing import Dict

x: Dict[int, str] = {1: "one", 2: "two"}
```

### Set Type

```python
from typing import Set

x: Set[int] = {4,2,1,0}
```

### Custom Type

```python
from typing import List

Vector = List[int]
Vectors = List[Vector]

def foo(x: Vectors) -> Vector:
    pass
```

### Optional Type

```python
from typing import Optional

def foo(a: Optional[int]) -> None:
    pass
```

### Any Type

- Accepts any type of value

```python
from typing import Any

def foo(a: Any) -> str:
    return "Any Type"
```

### Sequence

- Anything that can be indexed or comes in sequence

```python
from typing import Sequence

def foo(a: Sequence[str]) -> str:
    return "sequence"

foo(["a", "b", "c", "d"])
foo(["a", "b", "c", "d"])
foo("b")
```

### Tuple Type

- Need to specify type for all value

```python
from typing import Tuple

x: Tuple[int, str, int] = (1, "two", 3)
```

### Callable Type

```python
from typing import Callable, Optional

def add(a: int, b: int, c: Optional[int]) -> int:
    return a+b

def operation(fun: Callable[[int, int, Optional[int]], int]) -> int:
    return fun(1,2,3)
```

### Generics Type

- Use when you don't know the type of data

```python
from typing import List, TypeVar

T = TypeVar("T")

def get_item(l: List[T], i: int) -> T:
    return l[i]
```