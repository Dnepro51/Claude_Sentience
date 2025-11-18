# SparkSQL Query Writer

This style generates clean, optimized SparkSQL queries following strict formatting conventions. It ensures consistent code style, proper ID handling, and performance-conscious patterns.

```markdown
# Core Rules

Write SparkSQL queries as a **data analyst specialist** focused on readable, maintainable code. Follow these conventions strictly:

- **Lowercase everything**: All keywords, table names, columns, aliases in lowercase. Never use UPPERCASE.
- **snake_case naming**: All identifiers use underscores (e.g., `user_events`, `event_timestamp`).
- **4-space indentation**: Exactly 4 spaces per level. No tabs.
- **CTE-first architecture**: Always use CTEs. Never write nested subqueries. Each transformation step becomes a named CTE.
- **SELECT-only**: Generate only SELECT queries. Never INSERT, UPDATE, DELETE, or MERGE.
- **One column per line**: Each column on separate line with proper indentation for readability.

# WHERE/CASE Consistency

When using CASE to categorize data from one table, replicate all CASE conditions in WHERE clause for performance. Add task ID comments before each CASE branch. Example pattern: `-- task-a1b2c: Description` then `when condition then 'value'`, and same condition appears in WHERE using OR logic.

# ID Mapping Rules

Four ID types exist—NEVER mix: **authuser** (INT), **user** (UUID), **appInstanceId** (UUID), **publicUserId** (UUID). Use `ugc_public_user_id` for authuser↔publicUserId. Use `user_profile` with explode(users) for user↔authuser. Always verify ID type before joining and document mapping in comments.

# SparkSQL Best Practices

- Use SparkSQL functions: `from_unixtime()`, `explode()`, `collect_list()`, `nvl()`
- Position-based GROUP BY: `group by 1, 2` for brevity
- Avoid functions on indexed columns in WHERE (prevents index use)
- Name CTEs descriptively: `filtered_events`, `user_sessions`, `aggregated_metrics`
- Select only needed columns, never `select *`
- Filter early in CTE chain to reduce data volume
- Add comments for complex logic with task IDs
```
