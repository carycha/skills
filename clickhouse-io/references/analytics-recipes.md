# ClickHouse: Analytics Recipes

## Time Series Analysis

### Daily Active Users (DAU)
```sql
SELECT
    toDate(timestamp) AS date,
    uniq(user_id) AS dau
FROM events
WHERE timestamp >= today() - INTERVAL 30 DAY
GROUP BY date ORDER BY date;
```

## Retention Analysis

### Day N Retention
```sql
SELECT
    signup_date,
    countIf(days_since_signup = 0) AS day_0,
    countIf(days_since_signup = 1) AS day_1,
    countIf(days_since_signup = 7) AS day_7
FROM (
    SELECT
        user_id,
        min(toDate(timestamp)) OVER (PARTITION BY user_id) AS signup_date,
        toDate(timestamp) AS activity_date,
        dateDiff('day', signup_date, activity_date) AS days_since_signup
    FROM events
) GROUP BY signup_date ORDER BY signup_date DESC;
```

## Funnel Analysis

### Multi-step Conversion
```sql
SELECT
    countIf(step = 'viewed') AS viewed,
    countIf(step = 'clicked') AS clicked,
    countIf(step = 'purchased') AS purchased,
    round(clicked / viewed * 100, 2) AS view_to_click_rate
FROM (
    SELECT user_id, session_id, event_type AS step
    FROM events WHERE event_date = today()
) GROUP BY session_id;
```

## Cohort Analysis

### User Cohorts by Signup Month
```sql
SELECT
    toStartOfMonth(signup_date) AS cohort,
    toStartOfMonth(activity_date) AS month,
    dateDiff('month', cohort, month) AS months_since_signup,
    count(DISTINCT user_id) AS active_users
FROM (
    SELECT
        user_id,
        min(toDate(timestamp)) OVER (PARTITION BY user_id) AS signup_date,
        toDate(timestamp) AS activity_date
    FROM events
) GROUP BY cohort, month, months_since_signup ORDER BY cohort, months_since_signup;
```
