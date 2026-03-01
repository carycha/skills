# uv: Project Setup & Python Management

## Initialization
Initialize new Python projects with optimized defaults.

```bash
uv init my-app             # Application project
uv init my-lib --lib      # Library project
uv init --script script.py # Standalone script with inline metadata
```

## Python Version Management
uv can manage Python installations automatically.

```bash
uv python list           # List available Python versions
uv python install 3.12   # Install a specific version
uv python pin 3.11       # Pin the current project to a version
uv python upgrade --all  # Upgrade all managed installations
```

## Virtual Environment Syncing
Keep your virtual environment in sync with `pyproject.toml` and `uv.lock`.

```bash
uv sync                   # Sync all dependencies
uv sync --no-dev         # Sync excluding development dependencies
uv sync --all-extras     # Include all optional extras
uv sync --refresh        # Force a refresh of the environment
```

## Project Versioning
Manage your project's version metadata.

```bash
uv version               # Show current version
uv version 1.2.3         # Set specific version
uv version --bump minor  # Bump minor version (e.g., 0.1.0 -> 0.2.0)
```
