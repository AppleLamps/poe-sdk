# Errors

Poe uses standard HTTP status codes and returns a consistent JSON error body.

## Error body format

```json
{
  "error": {
    "message": "Human-readable error message",
    "type": "error_type",
    "code": "error_code"
  }
}
```

Some OpenAI-compatibility documentation also describes an error shape where `error.code` is numeric and may include `metadata`.

## Common HTTP status codes

- `400` Bad Request
- `401` Unauthorized (missing/invalid API key)
- `403` Forbidden
- `404` Not Found
- `408` Timeout
- `413` Request too large (context exceeded)
- `429` Rate limit exceeded
- `500` Internal server error
- `502` Upstream error
- `503` Service unavailable
- `529` Overloaded

## Common Error Types

### Authentication Errors (401)

- **Invalid API Key**: `invalid_api_key`. Verify your key in the `Authorization` header.

### Bad Request Errors (400)

- **Invalid Model**: `model_not_found`. Check `client.models.list()`.
- **Invalid Parameters**: `invalid_parameter`. Review endpoint documentation.
- **Missing Required Fields**: `missing_parameter`.

### Rate Limit Errors (429)

- **Rate Limit Exceeded**: `rate_limit_exceeded`. Implement exponential backoff.

### Insufficient Points (402)

- **Insufficient Points**: `insufficient_points`. Check balance with `client.usage.current_balance()`.

## Recommended SDK exception mapping

A typical Python SDK maps these into exceptions:

- `AuthenticationError` (401)
- `InsufficientCreditsError` (402)
- `PermissionError` (403)
- `NotFoundError` (404)
- `TimeoutError` (408)
- `RequestTooLargeError` (413)
- `RateLimitError` (429)
- `ServerError` (5xx, 529)

## Retry guidance

- Respect `Retry-After` when present.
- Use exponential backoff with jitter for `429` and transient `5xx` errors.
- Re-submit the exact same payload when retrying.
