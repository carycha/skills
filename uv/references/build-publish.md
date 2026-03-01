# uv: Building & Publishing

## Distributions
Build source and binary distributions (wheels).

```bash
uv build                 # Build .tar.gz and .whl
```

## Publishing to PyPI
Securely upload your packages to PyPI or other indices.

```bash
uv publish               # Publish to PyPI
uv publish --index-url https://test.pypi.org/legacy/ # To TestPyPI
```

## Authentication
Manage credentials for package indices.

```bash
uv auth login            # Login to a package index
uv auth logout           # Logout
uv auth status           # View current authentication status
```
