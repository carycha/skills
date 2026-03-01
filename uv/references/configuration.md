# uv: Configuration & Templates

## Standard pyproject.toml
A clean template optimized for uv.

```toml
[project]
name = "my-project"
version = "0.1.0"
description = "A high-performance Python project"
readme = "README.md"
requires-python = ">=3.9"
dependencies = [
    "requests>=2.31.0",
]

[project.optional-dependencies]
ml = [
    "scikit-learn>=1.0.0",
]

[dependency-groups]
dev = [
    "pytest>=7.0.0",
    "ruff>=0.1.0",
]
```

## Best Practices
- **Explicit Constraints**: Use `>=` or `~=` to balance compatibility and stability.
- **Dependency Groups**: Use `[dependency-groups]` for development tools instead of `extras`.
- **Formatting**: Use `uv format` to maintain consistent code style across the project.
```bash
uv format                # Format code
uv format --check        # Check without changing
```
