# Python Testing: Advanced Topics

## Testing Async Code

Requires `pytest-asyncio`.

```python
import pytest

@pytest.mark.asyncio
async def test_async_function():
    result = await async_add(2, 3)
    assert result == 5

# Async Fixture
@pytest.fixture
async def async_client():
    async with app.test_client() as client:
        yield client
```

## Testing Exceptions

```python
def test_divide_by_zero():
    with pytest.raises(ZeroDivisionError):
        divide(10, 0)

# Testing custom attributes
def test_exception_with_details():
    with pytest.raises(CustomError) as exc_info:
        raise CustomError("error", code=400)
    assert exc_info.value.code == 400
```

## Side Effects: Files and Directories

### tmp_path fixture (Preferred)

```python
def test_with_tmp_path(tmp_path):
    test_file = tmp_path / "test.txt"
    test_file.write_text("hello world")
    
    result = process_file(str(test_file))
    assert result == "hello world"
```

### Manual temp files

```python
import tempfile
import os

def test_file_processing():
    with tempfile.NamedTemporaryFile(mode='w', delete=False) as f:
        f.write("test content")
        temp_path = f.name
    try:
        assert process_file(temp_path) == "processed"
    finally:
        os.unlink(temp_path)
```
