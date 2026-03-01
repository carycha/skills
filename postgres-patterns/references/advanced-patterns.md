# PostgreSQL: Advanced Patterns

## Row Level Security (RLS)
Always wrap `auth.uid()` calls in a `SELECT` subquery for performance.
```sql
CREATE POLICY policy ON orders
  USING ((SELECT auth.uid()) = user_id);
```

## Upsert & Concurrency

### UPSERT (ON CONFLICT)
```sql
INSERT INTO settings (user_id, key, value)
VALUES (123, 'theme', 'dark')
ON CONFLICT (user_id, key)
DO UPDATE SET value = EXCLUDED.value;
```

### Queue Processing (SKIP LOCKED)
Efficiently process background jobs without row contention.
```sql
UPDATE jobs SET status = 'processing'
WHERE id = (
  SELECT id FROM jobs WHERE status = 'pending'
  ORDER BY created_at LIMIT 1
  FOR UPDATE SKIP LOCKED
) RETURNING *;
```

## Pagination

### Cursor-Based (Recommended)
O(1) complexity, unlike OFFSET which is O(n).
```sql
SELECT * FROM products WHERE id > $last_id ORDER BY id LIMIT 20;
```

## System Configuration Template

```sql
-- Performance (adjust based on RAM)
ALTER SYSTEM SET max_connections = 100;
ALTER SYSTEM SET work_mem = '8MB';

-- Reliability
ALTER SYSTEM SET idle_in_transaction_session_timeout = '30s';
ALTER SYSTEM SET statement_timeout = '30s';

-- Monitoring
CREATE EXTENSION IF NOT EXISTS pg_stat_statements;

-- Security
REVOKE ALL ON SCHEMA public FROM public;

SELECT pg_reload_conf();
```
