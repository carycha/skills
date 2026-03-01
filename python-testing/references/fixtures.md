# Python Testing: Fixtures

## Basic Fixture Usage

```python
import pytest

@pytest.fixture
def sample_data():
    return {"name": "Alice", "age": 30}

def test_sample_data(sample_data):
    assert sample_data["name"] == "Alice"
```

## Setup/Teardown

```python
@pytest.fixture
def database():
    # Setup
    db = Database(":memory:")
    db.create_tables()
    
    yield db  # Provide to test
    
    # Teardown
    db.close()
```

## Fixture Scopes

- `function` (default): Runs for each test.
- `module`: Runs once per module.
- `session`: Runs once per test session.

```python
@pytest.fixture(scope="session")
def shared_resource():
    resource = ExpensiveResource()
    yield resource
    resource.cleanup()
```

## Parameterized Fixtures

```python
@pytest.fixture(params=["sqlite", "postgresql"])
def db(request):
    return Database(request.param)
```

## Shared Fixtures (conftest.py)

Place `conftest.py` in your test directory to share fixtures across multiple modules.

```python
# tests/conftest.py
@pytest.fixture
def client():
    app = create_app(testing=True)
    with app.test_client() as client:
        yield client
```
