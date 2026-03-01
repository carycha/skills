---
name: postgres-patterns
description: PostgreSQL patterns for query optimization, schema design, indexing, and security. Use when writing SQL migrations, designing schemas, troubleshooting slow queries, or implementing Row Level Security (RLS) policies based on Supabase best practices.
---

# PostgreSQL Patterns

Best practices and patterns for building robust and performant PostgreSQL databases.

## Core Principles

- **Performance-First**: Design schemas and indexes for query efficiency from the start.
- **Data Integrity**: Use appropriate data types and constraints to ensure correctness.
- **Security by Design**: Implement Row Level Security (RLS) and follow least privilege principles.
- **Scalability**: Prefer cursor-based pagination and efficient concurrency patterns.

## Detailed Guidance

- **Indexing Strategies**: Index cheat sheet, composite index order, covering indexes, and partial indexes. See [indexing.md](references/indexing.md).
- **Schema Design & Anti-Patterns**: Data type recommendations and SQL scripts for detecting slow queries or missing indexes. See [schema-design.md](references/schema-design.md).
- **Advanced Patterns**: Row Level Security (RLS), UPSERT (ON CONFLICT), Skip Locked for queues, and configuration templates. See [advanced-patterns.md](references/advanced-patterns.md).

## Related Resources

- Agent: `database-reviewer` - Use for full database architecture reviews.
- Skill: `api-design` - For designing REST APIs that consume these database patterns.
