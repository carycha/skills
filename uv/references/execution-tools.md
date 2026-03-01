# uv: Execution & Tool Management

## Running Code
`uv run` automatically manages the virtual environment for you.

```bash
uv run python script.py         # Run a script in the project venv
uv run -m pytest               # Run a module (e.g., pytest)
uv run --env-file .env main.py # Load environment variables
```

### Temporary Dependencies
Run a script with a one-off dependency without adding it to `pyproject.toml`.
```bash
uv run --with requests script.py
```

## Running Tools (uvx)
`uvx` (uv extension) is a replacement for `pipx` to run tools in isolated environments.

```bash
uvx ruff check .               # Run ruff once
uvx --with ruff-lsp pyright    # Run with extra dependencies
```

## Global Tool Management
Install and manage CLI tools globally.

```bash
uv tool install ruff           # Install globally
uv tool list                   # List installed tools
uv tool upgrade ruff           # Upgrade a specific tool
uv tool uninstall ruff         # Remove a tool
```
