# Python Development Patterns: Logic & Flow

## Error Handling Patterns

### EAFP Style

Python prefers "Easier to Ask Forgiveness Than Permission" over "Look Before You Leap" (LBYL).

```python
# GOOD: EAFP style
def get_value(dictionary: dict, key: str) -> Any:
    try:
        return dictionary[key]
    except KeyError:
        return default_value
```

### Exception Best Practices

1. Catch specific exceptions.
2. Chain exceptions to preserve tracebacks.
3. Use custom exception hierarchies for domain errors.

```python
def load_config(path: str) -> Config:
    try:
        with open(path) as f:
            return Config.from_json(f.read())
    except FileNotFoundError as e:
        raise ConfigError(f"Config file not found: {path}") from e
    except json.JSONDecodeError as e:
        raise ConfigError(f"Invalid JSON in config: {path}") from e
```

## Context Managers

Always use `with` statements for resource management (files, network connections, locks).

```python
# Using contextlib for simple context managers
from contextlib import contextmanager

@contextmanager
def timer(name: str):
    start = time.perf_counter()
    yield
    elapsed = time.perf_counter() - start
    print(f"{name} took {elapsed:.4f} seconds")

# Class-based context managers (DatabaseTransaction)
class DatabaseTransaction:
    def __enter__(self):
        self.connection.begin_transaction()
        return self
    def __exit__(self, exc_type, exc_val, exc_tb):
        if exc_type is None: self.connection.commit()
        else: self.connection.rollback()
```

## Decorators

Use `functools.wraps` to preserve function metadata.

```python
import functools

def timer(func):
    @functools.wraps(func)
    def wrapper(*args, **kwargs):
        start = time.perf_counter()
        result = func(*args, **kwargs)
        print(f"{func.__name__} took {time.perf_counter() - start:.4f}s")
        return result
    return wrapper
```

## Data Containers

### Dataclasses

Preferred for mutable state and auto-generated boilerplate.

```python
from dataclasses import dataclass, field

@dataclass
class User:
    id: str
    name: str
    created_at: datetime = field(default_factory=datetime.now)

    def __post_init__(self):
        if "@" not in self.email:
            raise ValueError("Invalid email")
```

### NamedTuples

Preferred for immutable values and duck-typing as tuples.

```python
from typing import NamedTuple

class Point(NamedTuple):
    x: float
    y: float
```
