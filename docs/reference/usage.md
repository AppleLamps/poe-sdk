# Usage

The Usage API provides endpoints to check balance and retrieve points history.

## Current balance

**HTTP**: `GET https://api.poe.com/usage/current_balance`

### Method (current balance)

```python
def current_balance(self) -> CurrentBalance:
    ...
```

### Returns (current balance)

```json
{
  "current_point_balance": 295932027
}
```

## Points history

**HTTP**: `GET https://api.poe.com/usage/points_history`

### Method (points history)

```python
def points_history(
    self,
    *,
    limit: int = 20,
    starting_after: str | None = None,
) -> PointsHistoryPage:
    ...
```

### Parameters

- **`limit`**: 1–100 (default 20)
- **`starting_after`**: cursor; use the `query_id` from the last entry of the previous page

### Returns (points history)

A page object like:

```json
{
  "has_more": true,
  "length": 5,
  "data": [
    {
      "creation_time": 1761523099056852,
      "bot_name": "Claude-Sonnet-4.5",
      "query_id": "ltol8bhnkya9ak3twt",
      "usage_type": "API",
      "cost_points": 6554
    }
  ]
}
```

**Field descriptions:**

- `bot_name`: Name of the bot or model used.
- `creation_time`: Unix timestamp in microseconds.
- `query_id`: Unique identifier for pagination.
- `cost_points`: Points consumed by this query.
- `usage_type`: Descriptor for where points were used (e.g., `API`, `Chat`, `Canvas App`).
- `chat_name`: Chat name (populated if `usage_type` is `Chat`).
- `App name`: Canvas app name (populated if `usage_type` is `Canvas App`).

### Notes

- Entries are returned most-recent-first.
- Data is available for up to 30 days.
