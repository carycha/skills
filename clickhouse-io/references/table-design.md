# ClickHouse: Table Design Patterns

## MergeTree Engine (Standard)
The core engine for analytical tasks. Optimize with correct partitioning and ordering keys.

```sql
CREATE TABLE markets_analytics (
    date Date,
    market_id String,
    volume UInt64,
    trades UInt32,
    created_at DateTime
) ENGINE = MergeTree()
PARTITION BY toYYYYMM(date)
ORDER BY (date, market_id);
```

## ReplacingMergeTree (Deduplication)
Used when the same row might be inserted multiple times (e.g., re-running ETL).

```sql
CREATE TABLE user_events (
    event_id String,
    user_id String,
    timestamp DateTime,
    properties String
) ENGINE = ReplacingMergeTree()
ORDER BY (user_id, event_id, timestamp)
PRIMARY KEY (user_id, event_id);
```

## AggregatingMergeTree (Pre-aggregation)
For maintaining real-time aggregated metrics efficiently.

```sql
CREATE TABLE market_stats_hourly (
    hour DateTime,
    market_id String,
    total_volume AggregateFunction(sum, UInt64),
    unique_users AggregateFunction(uniq, String)
) ENGINE = AggregatingMergeTree()
ORDER BY (hour, market_id);

-- Query aggregated data using *Merge functions
SELECT
    hour,
    sumMerge(total_volume) AS volume,
    uniqMerge(unique_users) AS users
FROM market_stats_hourly
GROUP BY hour, market_id;
```

## Best Practices: Schema
- **Partitioning**: Partition by time (month/day), avoid > 100 partitions.
- **Ordering Key**: Put most frequently filtered columns first.
- **Data Types**: Use smallest appropriate type (UInt32 vs UInt64), `LowCardinality` for repeated strings, and `Enum` for categories.
