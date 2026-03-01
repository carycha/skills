# Python Development Patterns: Performance

## Lazy Evaluation

### Generator Expressions

Use generators for large datasets to avoid high memory overhead.

```python
# GOOD: Generator for lazy evaluation
total = sum(x * x for x in range(1_000_000))

# BAD: Creates large intermediate list
total = sum([x * x for x in range(1_000_000)])
```

### Generator Functions

```python
def read_large_file(path: str) -> Iterator[str]:
    """Read a large file line by line."""
    with open(path) as f:
        for line in f:
            yield line.strip()
```

## Concurrency Patterns

Choose the right tool based on the task:

| Pattern | Task Type | Best Tool |
|---------|-----------|-----------|
| **Threads** | I/O-bound (API calls, DB queries) | `concurrent.futures.ThreadPoolExecutor` |
| **Processes**| CPU-bound (Data processing) | `concurrent.futures.ProcessPoolExecutor` |
| **Async** | Concurrent I/O (Web servers) | `asyncio` |

```python
# Async example
import asyncio
async def fetch_all(urls: list[str]):
    tasks = [fetch_async(url) for url in urls]
    return await asyncio.gather(*tasks)
```

## Memory Efficiency

### __slots__

Use `__slots__` to reduce memory usage in classes with many instances.

```python
class Point:
    __slots__ = ['x', 'y']
    def __init__(self, x, y):
        self.x, self.y = x, y
```

### String Operations

Avoid string concatenation in loops; use `"".join()` instead.

```python
# GOOD: O(n)
result = "".join(str(item) for item in items)

# BAD: O(n^2)
result = ""
for item in items: result += str(item)
```
