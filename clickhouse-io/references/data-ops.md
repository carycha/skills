# ClickHouse: Data Operations

## Ingestion Patterns

### ✅ Bulk Insert (Recommended)
ClickHouse performance is bottlenecked by the number of inserts, not the number of rows per insert. **Always batch.**

```typescript
// Example: Batch insert with values
async function bulkInsertTrades(trades: Trade[]) {
  const values = trades.map(t => `('${t.id}', '${t.market_id}', ${t.amount})`).join(',')
  await clickhouse.query(`INSERT INTO trades VALUES ${values}`)
}
```

### ❌ Avoid Individual Inserts
Small frequent inserts cause high CPU usage and slow down background merges.

## Materialized Views (MV)
MVs are triggers that automatically aggregate or transform data during insertion.

```sql
-- Create MV for real-time aggregation
CREATE MATERIALIZED VIEW market_stats_hourly_mv
TO market_stats_hourly
AS SELECT
    toStartOfHour(timestamp) AS hour,
    market_id,
    sumState(amount) AS total_volume,
    uniqState(user_id) AS unique_users
FROM trades
GROUP BY hour, market_id;
```

## Data Pipeline Patterns

### ETL Pipeline
Periodic batch extraction from sources (e.g., PostgreSQL) to ClickHouse for analytical offloading.

```typescript
async function etlPipeline() {
  const rawData = await extractFromSource()
  const transformed = transformForOLAP(rawData)
  await bulkInsertToClickHouse(transformed)
}
```

### CDC Pattern
Real-time synchronization using change capture mechanisms. Use a message queue like Kafka for high-volume data streams.
