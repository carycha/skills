# PostgreSQL: Indexing Strategies

## Index Cheat Sheet

Choose the right index type based on your query patterns:

| Query Pattern | Index Type | Example |
|--------------|------------|---------|
| `WHERE col = value` | B-tree (default) | `CREATE INDEX idx ON t (col)` |
| `WHERE col > value` | B-tree | `CREATE INDEX idx ON t (col)` |
| `WHERE a = x AND b > y` | Composite | `CREATE INDEX idx ON t (a, b)` |
| `WHERE jsonb @> '{}'` | GIN | `CREATE INDEX idx ON t USING gin (col)` |
| `WHERE tsv @@ query` | GIN | `CREATE INDEX idx ON t USING gin (col)` |
| Time-series ranges | BRIN | `CREATE INDEX idx ON t USING brin (col)` |

## Advanced Index Patterns

### Composite Index Order
Equality columns should come first, then range columns.
```sql
CREATE INDEX idx ON orders (status, created_at);
-- Optimized for: WHERE status = 'pending' AND created_at > '2024-01-01'
```

### Covering Index (Index Only Scan)
Use the `INCLUDE` clause to avoid table lookups for frequently selected columns.
```sql
CREATE INDEX idx ON users (email) INCLUDE (name, created_at);
-- Covers: SELECT email, name, created_at FROM users WHERE email = ?
```

### Partial Index
Create smaller, faster indexes by filtering the rows included.
```sql
CREATE INDEX idx ON users (email) WHERE deleted_at IS NULL;
-- Only indexes active users
```

### Concurrent Indexing
Always use `CONCURRENTLY` in production migrations to avoid locking tables.
```sql
CREATE INDEX CONCURRENTLY idx_users_email ON users (email);
```
