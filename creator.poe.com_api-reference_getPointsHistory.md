---
url: "https://creator.poe.com/api-reference/getPointsHistory"
title: "Get usage history | Poe Creator Platform"
---

# Get usage history

GET`https://api.poe.com/usage/points_history`

Code example

Inspect recent API activity with pagination and timestamped entries.

cURL

cURL

```
curl https://api.poe.com/usage/points_history?limit=20&starting_after=value \
-H "Authorization: Bearer sk_test_51SAMPLEKEY" \
-H "Accept: application/json"
```

Example history

```json
{
"has_more": true,
"length": 5,
"data": [\
  {\
    "creation_time": 1761523099056852,\
    "bot_name": "Claude-Sonnet-4.5",\
    "query_id": "ltol8bhnkya9ak3twt",\
    "usage_type": "API",\
    "cost_points": 6554\
  },\
  {\
    "creation_time": 1761523092991619,\
    "bot_name": "Claude-Sonnet-4.5",\
    "query_id": "ltoklyofyfiix6j6nf",\
    "usage_type": "API",\
    "cost_points": 6683\
  },\
  {\
    "creation_time": 1761523092861446,\
    "bot_name": "Claude-Haiku-4.5",\
    "query_id": "ltokml8l916tc7gfxu",\
    "usage_type": "API",\
    "cost_points": 56\
  }\
]
}
```

## [Overview](https://creator.poe.com/api-reference/getPointsHistory\#overview)

Retrieve your usage history with detailed information about each API call.

**Features:**

- Entries are fetched by creation time, descending (most recent first)
- Pagination support via `starting_after` cursor
- Data available for up to 30 days
- Maximum 100 entries per request

## [Authentication](https://creator.poe.com/api-reference/getPointsHistory\#authentication)

Send your Poe API key in the `Authorization` header:

```
Authorization: Bearer sk_test_51SAMPLEKEY
```

All requests must be made over HTTPS.

## [Parameters](https://creator.poe.com/api-reference/getPointsHistory\#parameters)

| Name | Location | Type | Required | Description |
| --- | --- | --- | --- | --- |
| `limit` | query | integer | Optional | Number of entries to return (max 100, default 20) Min: 1 · Max: 100 · Default: `20` |
| `starting_after` | query | string | Optional | Pagination cursor - use the query\_id from the last entry of a previous response |

## [Responses](https://creator.poe.com/api-reference/getPointsHistory\#responses)

| Field | Type | Required | Description |
| --- | --- | --- | --- |
| `has_more` | boolean | Optional | Whether there are more entries available for pagination |
| `length` | integer | Optional | Number of entries in the current response |
| `data` | object\[\] | Optional |  |
| `data[].creation_time` | int64 | **Required** | Unix timestamp in microseconds when the query was created |
| `data[].bot_name` | string | **Required** | Name of the bot or model used |
| `data[].query_id` | string | **Required** | Unique identifier for the query (used for pagination) |
| `data[].usage_type` | "API" \| "Chat" \| "Canvas App" | **Required** | Descriptor for where the points were used Allowed values: `API`, `Chat`, `Canvas App` |
| `data[].cost_points` | integer | **Required** | Number of points consumed by this query |

## [❌ Error codes](https://creator.poe.com/api-reference/getPointsHistory\#-error-codes)

| Http | Type | Description |
| --- | --- | --- |
| 401 | `authentication_error` | Authentication failed Invalid API key |

## [Best Practices](https://creator.poe.com/api-reference/getPointsHistory\#best-practices)

Use the `starting_after` cursor for pagination. The `query_id` from the last entry can be used to fetch the next page of results.

Implement pagination for large result sets:

- Start with a reasonable `limit` (20-50 entries)
- Use `has_more` to determine if more pages exist
- Pass the last `query_id` as `starting_after` for next page
- Data is available for 30 days

## [🔁 Callbacks & webhooks](https://creator.poe.com/api-reference/getPointsHistory\#-callbacks--webhooks)

No callbacks or webhooks are associated with this endpoint.

Code example

Inspect recent API activity with pagination and timestamped entries.

cURL

cURL

```
curl https://api.poe.com/usage/points_history?limit=20&starting_after=value \
-H "Authorization: Bearer sk_test_51SAMPLEKEY" \
-H "Accept: application/json"
```

Example history

```json
{
"has_more": true,
"length": 5,
"data": [\
  {\
    "creation_time": 1761523099056852,\
    "bot_name": "Claude-Sonnet-4.5",\
    "query_id": "ltol8bhnkya9ak3twt",\
    "usage_type": "API",\
    "cost_points": 6554\
  },\
  {\
    "creation_time": 1761523092991619,\
    "bot_name": "Claude-Sonnet-4.5",\
    "query_id": "ltoklyofyfiix6j6nf",\
    "usage_type": "API",\
    "cost_points": 6683\
  },\
  {\
    "creation_time": 1761523092861446,\
    "bot_name": "Claude-Haiku-4.5",\
    "query_id": "ltokml8l916tc7gfxu",\
    "usage_type": "API",\
    "cost_points": 56\
  }\
]
}
```