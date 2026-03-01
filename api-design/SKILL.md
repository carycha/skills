---
name: api-design
description: REST API design patterns for production-grade APIs. Use when designing new endpoints, reviewing contracts, or implementing pagination, filtering, error handling, versioning, and rate limiting to ensure consistency and developer-friendliness.
---

# API Design Patterns

Best practices for designing consistent, developer-friendly REST APIs.

## Core Principles

- **Developer-Friendly**: APIs should be intuitive and easy to use.
- **Predictable**: Follow standard HTTP semantics and naming conventions.
- **Secure**: Implement robust authentication and authorization.
- **Scalable**: Use appropriate pagination and rate limiting.

## Detailed Guidance

- **Core Design**: URL structure, naming rules, HTTP methods, status codes, response formats, and pagination. See [design-patterns.md](references/design-patterns.md).
- **Security & Operations**: Authentication, authorization patterns, rate limiting, and versioning strategies. See [security-ops.md](references/security-ops.md).
- **Implementation**: Practical code examples in TypeScript (Next.js), Python (DRF), and Go. See [implementation.md](references/implementation.md).
- **Checklist**: Final verification list before shipping a new endpoint. See [checklist.md](references/checklist.md).
