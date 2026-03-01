# uv: Dependency Management

## Adding & Removing Packages
High-performance dependency management.

```bash
uv add requests           # Add to main dependencies
uv add --dev pytest       # Add to development group
uv add --optional ml torch # Add to optional 'ml' extra
uv remove requests        # Remove a package
```

## Inspection & Locking
Understand and freeze your dependency graph.

```bash
uv tree                   # Display dependency tree
uv lock                   # Update uv.lock without installing
```

## Exporting
Export to standard formats for compatibility or CI systems.

```bash
uv export > requirements.txt           # Export to requirements.txt
uv export --no-dev > requirements.txt  # Production-only export
```

## Tips for Reproducibility
- Always commit `uv.lock` to your version control.
- Use `uv sync --locked` in CI environments to ensure exact matches.
