# Python Development Patterns: Typing

## Modern Type Hints (Python 3.9+)

Python 3.9+ uses built-in types for collections, making `typing.List`, `typing.Dict`, etc., unnecessary.

```python
# GOOD: Modern style (3.9+)
def process_items(items: list[str]) -> dict[str, int]:
    return {item: len(item) for item in items}

# LEGACY: Python 3.8 and earlier
from typing import List, Dict
def process_items(items: List[str]) -> Dict[str, int]:
    return {item: len(item) for item in items}
```

### Basic Type Annotations

```python
from typing import Optional, Any

def process_user(
    user_id: str,
    data: dict[str, Any],
    active: bool = True
) -> Optional[User]:
    """Process a user and return the updated User or None."""
    if not active:
        return None
    return User(user_id, data)
```

## Type Aliases and TypeVar

```python
from typing import TypeVar, Union

# Type alias for complex types
JSON = Union[dict[str, Any], list[Any], str, int, float, bool, None]

def parse_json(data: str) -> JSON:
    return json.loads(data)

# Generic types
T = TypeVar('T')

def first(items: list[T]) -> T | None:
    """Return the first item or None if list is empty."""
    return items[0] if items else None
```

## Protocol-Based Duck Typing

Protocols allow structural subtyping, specifying what an object *does* rather than what it *is*.

```python
from typing import Protocol

class Renderable(Protocol):
    def render(self) -> str:
        """Render the object to a string."""

def render_all(items: list[Renderable]) -> str:
    """Render all items that implement the Renderable protocol."""
    return "
".join(item.render() for item in items)
```
