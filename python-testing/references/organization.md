# Python Testing: Organization & Best Practices

## Directory Structure

```
tests/
├── conftest.py          # Shared fixtures
├── unit/                # Unit tests
│   ├── test_models.py
│   └── test_utils.py
├── integration/         # Integration tests
│   └── test_api.py
└── e2e/                 # End-to-end tests
```

## Test Classes

Grouping related tests in a class.

```python
class TestUserService:
    @pytest.fixture(autouse=True)
    def setup(self):
        self.service = UserService()

    def test_create_user(self):
        user = self.service.create_user("Alice")
        assert user.name == "Alice"
```

## Configuration

### pyproject.toml (Modern)

```toml
[tool.pytest.ini_options]
testpaths = ["tests"]
python_files = ["test_*.py"]
addopts = [
    "--strict-markers",
    "--cov=mypackage",
    "--cov-report=term-missing",
]
markers = [
    "slow: marks tests as slow",
    "integration: marks tests as integration tests",
]
```

## Coverage Requirements

- **Target**: 80%+ code coverage.
- **Critical paths**: 100% coverage required.

```bash
# Run with coverage
pytest --cov=mypackage --cov-report=html
```

## Best Practices (DO/DON'T)

### DO
- **Follow TDD**: Red-Green-Refactor.
- **Test behavior**, not implementation.
- **Mock external dependencies** (DB, APIs).
- **Test edge cases** (None, empty, boundary).

### DON'T
- **Don't share state** between tests.
- **Don't catch exceptions** in tests; use `pytest.raises`.
- **Don't ignore failures**.
