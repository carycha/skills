# Python Testing: pytest Fundamentals

## Basic Test Structure

```python
import pytest

def test_addition():
    """Test basic addition."""
    assert 2 + 2 == 4

def test_string_uppercase():
    """Test string uppercasing."""
    assert "hello".upper() == "HELLO"
```

## Assertions

```python
# Basic
assert result == expected
assert result is True
assert item in collection

# Exception testing (preferred)
with pytest.raises(ValueError, match="invalid input"):
    raise ValueError("invalid input provided")

# Check exception attributes
with pytest.raises(ValueError) as exc_info:
    raise ValueError("error message")
assert str(exc_info.value) == "error message"
```

## Markers and Test Selection

### Custom Markers

```python
@pytest.mark.slow
def test_heavy_computation():
    pass

@pytest.mark.integration
def test_api_call():
    pass
```

### Execution Commands

```bash
# Run specific markers
pytest -m "not slow"
pytest -m "integration or unit"

# Run tests by name pattern
pytest -k "user_login"

# Run until first failure
pytest -x
```

## Parametrization

```python
@pytest.mark.parametrize("input,expected", [
    ("hello", "HELLO"),
    ("world", "WORLD"),
], ids=["test-hello", "test-world"])
def test_uppercase(input, expected):
    assert input.upper() == expected
```
