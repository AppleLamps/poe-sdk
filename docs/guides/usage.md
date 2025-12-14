# Usage & Billing

Poe API usage consumes **points** from the Poe account associated with the API key.

## Current Balance

### Endpoint (Current Balance)

- `GET https://api.poe.com/usage/current_balance`

### Example

```python
import os
from poe_sdk import PoeClient

client = PoeClient(api_key=os.environ["POE_API_KEY"])

balance = client.usage.current_balance()
print(balance.current_point_balance)
```

## Points History

### Endpoint (Points History)

- `GET https://api.poe.com/usage/points_history`

### Query Parameters

- `limit`: max 100 (default 20)
- `starting_after`: cursor (`query_id` from last entry)

### Example (Pagination)

```python
import os
from poe_sdk import PoeClient

client = PoeClient(api_key=os.environ["POE_API_KEY"])

page = client.usage.points_history(limit=50)
print(page.length, page.has_more)

while page.has_more and page.data:
    cursor = page.data[-1].query_id
    page = client.usage.points_history(limit=50, starting_after=cursor)
    print(page.length, page.has_more)
```

## Notes

- Usage history is available for up to **30 days** (documented).
- Entries are returned most-recent-first.
