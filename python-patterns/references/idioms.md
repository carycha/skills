# Python Development Patterns: Idioms & Anti-Patterns

## Core Idioms

| Idiom | Recommendation |
|-------|----------------|
| **`enumerate`** | Use `for i, x in enumerate(items)` for index/value. |
| **`is` for `None`** | Always use `if x is None:` or `if x is not None:`. |
| **`pathlib.Path`** | Prefer `pathlib` over `os.path` for path manipulations. |
| **f-strings** | Use `f"{name}"` (3.6+) for readability and speed. |
| **`isinstance`** | Prefer `isinstance(x, list)` over `type(x) == list`. |

## Anti-Patterns to Avoid

### Mutable Default Arguments

Default arguments are evaluated once at definition time.

```python
# BAD: items will persist across calls
def append_to(item, items=[]):
    items.append(item)
    return items

# GOOD: Use None as default
def append_to(item, items=None):
    if items is None: items = []
    items.append(item)
    return items
```

### Bare Except

Never use `except: pass`; it hides bugs and system exit signals.

```python
# BAD
try: risky()
except: pass

# GOOD
try: risky()
except SpecificError as e: logger.error(e)
```

### List Comprehension Complexity

Don't overcomplicate list comprehensions; use a loop or generator function if it becomes unreadable.

```python
# BAD: Too complex
result = [x * 2 for x in items if x > 0 if x % 2 == 0]

# GOOD: Break it down
def filter_and_transform(items):
    for x in items:
        if x > 0 and x % 2 == 0: yield x * 2
```
