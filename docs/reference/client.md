# Client

This SDK is organized around a `PoeClient` that exposes grouped namespaces:

- `client.chat.completions.create(...)`
- `client.models.list()`
- `client.usage.current_balance()`
- `client.usage.points_history(...)`

## `PoeClient`

```python
class PoeClient:
    def __init__(
        self,
        api_key: str | None = None,
        base_url: str = "https://api.poe.com",
        timeout: float | None = 30.0,
        default_headers: dict[str, str] | None = None,
    ) -> None:
        ...
```

- **`api_key`**: Poe API key from `https://poe.com/api_key`. Required for most endpoints.
- **`base_url`**: Defaults to `https://api.poe.com`.
- **`timeout`**: Request timeout (seconds).
- **`default_headers`**: Optional headers applied to every request.

### Leaderboard attribution headers

If you want Poe to attribute API requests to your external application:

- `HTTP-Referer`: URL linked from the leaderboard entry
- `X-Title`: display name

These can be supplied as `default_headers` or per-request `extra_headers`.

## Response headers

The Poe API includes useful headers such as:

- `x-request-id`
- `openai-processing-ms`
- `x-ratelimit-limit-requests`
- `x-ratelimit-remaining-requests`
- `x-ratelimit-reset-requests`

A production-ready SDK typically makes response headers accessible for debugging and rate limiting.
