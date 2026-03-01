# PostgreSQL: Schema Design & Anti-Patterns

## Recommended Data Types

| Use Case | Correct Type | Avoid | Reason |
|----------|-------------|-------|--------|
| IDs | `bigint` | `int`, UUID | Avoid integer overflow, random UUIDs hurt B-tree performance |
| Strings | `text` | `varchar(255)` | `text` has no performance penalty and more flexibility |
| Timestamps | `timestamptz` | `timestamp` | `timestamptz` handles timezones correctly |
| Money | `numeric(10,2)` | `float` | Exact precision for financial data |
| Flags | `boolean` | `varchar`, `int` | Semantic clarity and minimal storage |

## Anti-Pattern Detection

### Find Unindexed Foreign Keys
Unindexed foreign keys cause full table scans on deletes/updates to the parent table.
```sql
SELECT conrelid::regclass, a.attname
FROM pg_constraint c
JOIN pg_attribute a ON a.attrelid = c.conrelid AND a.attnum = ANY(c.conkey)
WHERE c.contype = 'f'
  AND NOT EXISTS (
    SELECT 1 FROM pg_index i
    WHERE i.indrelid = c.conrelid AND a.attnum = ANY(i.indkey)
  );
```

### Identify Slow Queries
Requires `pg_stat_statements` extension.
```sql
SELECT query, mean_exec_time, calls
FROM pg_stat_statements
WHERE mean_exec_time > 100
ORDER BY mean_exec_time DESC;
```

### Table Bloat & Dead Tuples
Monitor tables that need manual vacuuming.
```sql
SELECT relname, n_dead_tup, last_vacuum
FROM pg_stat_user_tables
WHERE n_dead_tup > 1000
ORDER BY n_dead_tup DESC;
```
