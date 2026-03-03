---
name: uv
description: UV Python Manager Expert. Use when initializing Python projects, managing dependencies, syncing virtual environments, running tools with `uvx`, or building/publishing distributions with the ultra-fast `uv` toolchain.
---

# uv

A high-performance Python package and project manager with integrated virtual environment and tool management.

## Core Principles

- **Performance**: 10-100x faster than traditional pip workflows.
- **Unified Workflow**: Manage Python versions, dependencies, and environments in one tool.
- **Isolation**: Tools and environments are kept separate to prevent dependency hell.
- **Reproducibility**: Strong focus on lockfiles (`uv.lock`) for consistent builds.

## Detailed Guidance

- **Project Setup & Python**: Initialization, version pinning, and environment syncing. See [project-setup.md](references/project-setup.md).
- **Dependency Management**: Adding/removing packages, locking, and dependency trees. See [dependencies.md](references/dependencies.md).
- **Execution & Tools**: `uv run`, `uvx`, and global tool management. See [execution-tools.md](references/execution-tools.md).
- **Building & Publishing**: Distribution builds, PyPI publishing, and authentication. See [build-publish.md](references/build-publish.md).
- **Configuration & Templates**: Standard `pyproject.toml` templates and formatting best practices. See [configuration.md](references/configuration.md).

## Quick Tips

- Use `uv run` to automatically handle venv activation.
- Use `uvx` for running CLI tools without permanent installation.
- Use `--with` for temporary dependencies during script execution.
