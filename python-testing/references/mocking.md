# Python Testing: Mocking and Patching

## Mocking Functions

```python
from unittest.mock import patch, Mock

@patch("mypackage.external_api_call")
def test_with_mock(api_call_mock):
    api_call_mock.return_value = {"status": "success"}
    result = my_function()
    
    api_call_mock.assert_called_once()
    assert result["status"] == "success"
```

## Mocking Context Managers

```python
@patch("builtins.open", new_callable=mock_open)
def test_file_reading(mock_file):
    mock_file.return_value.read.return_value = "file content"
    result = read_file("test.txt")
    
    mock_file.assert_called_once_with("test.txt", "r")
    assert result == "file content"
```

## Mocking Async Functions

Use `pytest-asyncio` and `assert_awaited_once()`.

```python
@pytest.mark.asyncio
@patch("mypackage.async_api_call")
async def test_async_mock(api_call_mock):
    api_call_mock.return_value = {"status": "ok"}
    result = await my_async_function()
    
    api_call_mock.assert_awaited_once()
    assert result["status"] == "ok"
```

## Autospec

Use `autospec=True` to catch API misuse.

```python
@patch("mypackage.DBConnection", autospec=True)
def test_autospec(db_mock):
    db = db_mock.return_value
    db.query("SELECT * FROM users")
```

## Mock Properties

```python
@pytest.fixture
def mock_config():
    config = Mock()
    type(config).debug = PropertyMock(return_value=True)
    return config
```
