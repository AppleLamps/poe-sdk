# Rate Limits

## Current limits

The documented rate limit is:

- **500 requests per minute (RPM)** per API key

## Rate limit headers

Every response includes request-based rate limit headers:

- `x-ratelimit-limit-requests` (e.g. `500`)
- `x-ratelimit-remaining-requests`
- `x-ratelimit-reset-requests` (seconds until reset)

Example:

```text
x-ratelimit-remaining-requests: 499
x-ratelimit-limit-requests: 500
x-ratelimit-reset-requests: 1
```

## Handling 429 responses

When exceeded, the API returns `429 Too Many Requests`.

Recommended strategy:

- Honor `Retry-After` if present.
- Otherwise apply exponential backoff (e.g. 250ms, 500ms, 1s...) with jitter.
- Add client-side throttling (token bucket, leaky bucket, or simple queue) for high-volume apps.

## Load Testing

**Do not load test production.** Use mocked endpoints to avoid consuming your rate limit.

- **Mock API Requests**: Build a configurable system to mock Poe API responses.
- **Simulate Latency**: Add realistic delays to mocked responses based on real API measurements.

## Usage Tracking

Use the Usage API to track detailed API usage:

- Historical usage data
- Request counts
- Point consumption

See `client.usage.points_history(...)` for details.

## Higher limits

If you need higher rate limits, contact `developers@poe.com` (documented).
