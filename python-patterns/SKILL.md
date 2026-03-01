---
name: python-patterns
description: Pythonic idioms, PEP 8 standards, and best practices. Use when writing, reviewing, or refactoring Python code, designing packages, or optimizing performance and memory usage to ensure robust and maintainable applications.
---

# Python Development Patterns

Idiomatic Python patterns and best practices for building robust, efficient, and maintainable applications.

## Core Principles

- **Readability Counts**: Python prioritizes code that is obvious and easy to understand.
- **Explicit is Better Than Implicit**: Avoid magic; be clear about what your code does.
- **EAFP**: "Easier to Ask Forgiveness Than Permission" - prefer exception handling over pre-checks.

## Detailed Guidance

- **Typing & Type Hints**: Modern Python (3.9+) type annotations, Protocols, Generics, and Type Aliases. See [typing.md](references/typing.md).
- **Logic & Flow**: Error handling best practices, Context Managers, Decorators, and Data Containers (Dataclasses, NamedTuples). See [logic-flow.md](references/logic-flow.md).
- **Performance & Memory**: Lazy evaluation with Generators, Concurrency patterns (Async, Threads, Processes), and memory efficiency (`__slots__`). See [performance.md](references/performance.md).
- **Structure & Tooling**: Project layout conventions, imports, and toolchain integration (`pyproject.toml`). See [structure.md](references/structure.md).
- **Idioms & Anti-Patterns**: Essential Pythonic idioms and common traps to avoid. See [idioms.md](references/idioms.md).
