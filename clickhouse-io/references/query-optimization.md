# ClickHouse: Query Optimization

## Efficient Filtering
ClickHouse is column-oriented; indexed filtering is crucial.

```sql
-- ✅ GOOD: Indexed columns first
SELECT * FROM markets_analytics
WHERE date >= '2025-01-01' AND market_id = 'market-123'
ORDER BY date DESC LIMIT 100;

-- ❌ BAD: Filter on non-indexed columns before indexed ones
SELECT * FROM markets_analytics
WHERE volume > 1000 AND market_name LIKE '%election%' AND date >= '2025-01-01';
```

## Aggregations
Use ClickHouse-specific aggregation functions for speed.

```sql
-- Special aggregation functions
SELECT
    toStartOfDay(created_at) AS day,
    sum(volume) AS total_volume,
    uniq(trader_id) AS unique_traders, -- HyperLogLog
    quantile(0.95)(trade_size) AS p95 -- Optimized percentile
FROM trades
GROUP BY day;
```

## Window Functions
Calculate running totals and relative metrics within partitions.

```sql
SELECT
    date, market_id, volume,
    sum(volume) OVER (
        PARTITION BY market_id ORDER BY date
        ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW
    ) AS cumulative_volume
FROM markets_analytics;
```

## Performance Monitoring

### Slow Query Log
```sql
SELECT
    query_id, user, query, query_duration_ms, read_rows, memory_usage
FROM system.query_log
WHERE type = 'QueryFinish' AND query_duration_ms > 1000
ORDER BY query_duration_ms DESC LIMIT 10;
```

### Table Statistics
```sql
SELECT
    table, formatReadableSize(sum(bytes)) AS size, sum(rows) AS rows
FROM system.parts
WHERE active GROUP BY table;
```
