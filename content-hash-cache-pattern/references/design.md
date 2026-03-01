# Design Decisions & Anti-Patterns

## Key Design Decisions

| Decision | Rationale |
|----------|-----------|
| **SHA-256 content hash** | Path-independent, auto-invalidates on content change |
| **`{hash}.json` file naming** | O(1) lookup, no index file needed |
| **Service layer wrapper** | SRP: extraction stays pure, cache is a separate concern |
| **Manual JSON serialization** | Full control over frozen dataclass serialization |
| **Corruption returns `None`** | Graceful degradation, re-processes on next run |
| **`cache_dir.mkdir(parents=True)`** | Lazy directory creation on first write |

## Anti-Patterns to Avoid

```python
# BAD: Path-based caching (breaks on file move/rename)
cache = {"/path/to/file.pdf": result}

# BAD: Adding cache logic inside the processing function (SRP violation)
def extract_text(path, *, cache_enabled=False, cache_dir=None):
    if cache_enabled:  # Now this function has two responsibilities
        ...

# BAD: Using dataclasses.asdict() with nested frozen dataclasses
# (can cause issues with complex nested types)
data = dataclasses.asdict(entry)  # Use manual serialization instead
```
