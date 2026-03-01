# Python Development Patterns: Structure & Tooling

## Standard Project Layout

Use a `src` layout to ensure tests run against the installed package.

```
myproject/
├── src/
│   └── mypackage/
│       ├── __init__.py
│       ├── main.py
│       └── models/
├── tests/
├── pyproject.toml
└── README.md
```

### Import Conventions

Order:
1. Standard library imports.
2. Third-party library imports.
3. Local application imports.

```python
import os
from pathlib import Path

import requests
from fastapi import FastAPI

from mypackage.models import User
```

## Tooling Integration

### Recommended pyproject.toml

Modern Python projects should consolidate configuration in `pyproject.toml`.

```toml
[project]
name = "mypackage"
requires-python = ">=3.9"
dependencies = ["requests>=2.31.0"]

[tool.black]
line-length = 88

[tool.ruff]
select = ["E", "F", "I", "N", "W"]

[tool.mypy]
disallow_untyped_defs = true

[tool.pytest.ini_options]
testpaths = ["tests"]
```

### Essential Toolchain

- **Formatting**: `black`, `isort`.
- **Linting**: `ruff` (extremely fast).
- **Type Checking**: `mypy`.
- **Testing**: `pytest` with `pytest-cov`.
- **Security**: `bandit`, `pip-audit`.
