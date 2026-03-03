---
name: clickhouse-io
description: ClickHouse & OLAP Expert. Use when designing high-performance analytical schemas (MergeTree), writing optimized SQL queries, implementing real-time dashboards, or migrating large datasets from relational databases for analytical workloads.
---

# ClickHouse Analytics Patterns

ClickHouse-specific patterns for high-performance analytics and data engineering.

## Core Principles

- **Column-Oriented**: Optimized for fast analytical queries on large datasets.
- **MergeTree First**: Use the MergeTree engine family for almost all analytical tables.
- **Batching is Key**: Always batch inserts to avoid performance degradation.
- **Materialize Early**: Use Materialized Views for real-time aggregations.

## Detailed Guidance

- **Table Design**: MergeTree engine selection, partitioning strategies, and ordering keys. See [table-design.md](references/table-design.md).
- **Query Optimization**: Efficient filtering, ClickHouse-specific aggregations, and performance monitoring. See [query-optimization.md](references/query-optimization.md).
- **Data Operations**: Batch/Streaming ingestion, Materialized Views, and ETL/CDC pipelines. See [data-ops.md](references/data-ops.md).
- **Analytics Recipes**: Ready-to-use SQL for time series, funnels, retention, and cohort analysis. See [analytics-recipes.md](references/analytics-recipes.md).

## Related Resources

- Skill: `postgres-patterns` - For initial transactional data design before offloading to ClickHouse.
- Skill: `api-design` - For building analytical APIs consuming ClickHouse data.
