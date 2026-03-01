---
name: python-testing
description: Python testing strategies using pytest, TDD methodology, fixtures, mocking, and coverage requirements. Use when writing new Python code (TDD), designing test suites, reviewing coverage, or setting up testing infrastructure to ensure code quality and reliability.
---

# Python Testing Patterns

Comprehensive testing strategies for Python applications using pytest, TDD methodology, and best practices.

## Core Testing Philosophy

### Test-Driven Development (TDD)

Always follow the TDD cycle:

1. **RED**: Write a failing test for the desired behavior.
2. **GREEN**: Write minimal code to make the test pass.
3. **REFACTOR**: Improve code while keeping tests green.

```python
# RED
def test_add():
    assert add(2, 3) == 5

# GREEN
def add(a, b):
    return a + b
```

## Detailed Guidance

- **pytest Fundamentals**: Test structure, assertions, markers, and test selection. See [pytest-basics.md](references/pytest-basics.md).
- **Fixtures**: Basic usage, setup/teardown, scopes, and sharing fixtures via conftest.py. See [fixtures.md](references/fixtures.md).
- **Mocking & Patching**: Mocking functions, classes, async code, and using autospec. See [mocking.md](references/mocking.md).
- **Advanced Topics**: Async testing, exception handling, and file/directory side effects. See [advanced.md](references/advanced.md).
- **Organization & Best Practices**: Directory layout, configuration (pytest.ini/pyproject.toml), and coverage requirements. See [organization.md](references/organization.md).
