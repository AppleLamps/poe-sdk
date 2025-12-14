---
url: "https://creator.poe.com/api-reference/errors"
title: "Error Handling | Poe Creator Platform"
---

# Error Handling

# [Error Handling](https://creator.poe.com/api-reference/errors\#error-handling)

The Poe API uses standard HTTP status codes to indicate the success or failure of requests. This guide helps you understand and handle errors effectively.

## [HTTP Status Codes](https://creator.poe.com/api-reference/errors\#http-status-codes)

The API returns the following status codes:

| Status Code | Meaning | Description |
| --- | --- | --- |
| `200` | OK | Request succeeded |
| `400` | Bad Request | Invalid request format or parameters |
| `401` | Unauthorized | Missing or invalid API key |
| `403` | Forbidden | Valid API key but insufficient permissions |
| `404` | Not Found | Resource not found |
| `429` | Too Many Requests | Rate limit exceeded |
| `500` | Internal Server Error | Server error - please retry |
| `503` | Service Unavailable | Service temporarily unavailable |

## [Error Response Format](https://creator.poe.com/api-reference/errors\#error-response-format)

All error responses follow a consistent JSON format:

```
{
  "error": {
    "message": "Human-readable error message",
    "type": "error_type",
    "code": "error_code"
  }
}
```

**Example Error Response:**

```
{
  "error": {
    "message": "Invalid API key provided",
    "type": "invalid_request_error",
    "code": "invalid_api_key"
  }
}
```

## [Common Error Types](https://creator.poe.com/api-reference/errors\#common-error-types)

### [Authentication Errors (401)](https://creator.poe.com/api-reference/errors\#authentication-errors-401)

**Invalid API Key:**

```
{
  "error": {
    "message": "Invalid API key provided",
    "type": "invalid_request_error",
    "code": "invalid_api_key"
  }
}
```

**Resolution:** Verify your API key is correct and properly formatted in the `Authorization` header.

### [Bad Request Errors (400)](https://creator.poe.com/api-reference/errors\#bad-request-errors-400)

**Invalid Model:**

```
{
  "error": {
    "message": "Model 'invalid-model' does not exist",
    "type": "invalid_request_error",
    "code": "model_not_found"
  }
}
```

**Resolution:** Check the [List Models](https://creator.poe.com/api-reference/listModels) endpoint for available models.

**Invalid Parameters:**

```
{
  "error": {
    "message": "Temperature must be between 0 and 2",
    "type": "invalid_request_error",
    "code": "invalid_parameter"
  }
}
```

**Resolution:** Review the endpoint documentation for valid parameter ranges.

**Missing Required Fields:**

```
{
  "error": {
    "message": "Missing required parameter: 'messages'",
    "type": "invalid_request_error",
    "code": "missing_parameter"
  }
}
```

**Resolution:** Ensure all required fields are included in your request.

### [Rate Limit Errors (429)](https://creator.poe.com/api-reference/errors\#rate-limit-errors-429)

```
{
  "error": {
    "message": "Rate limit exceeded. Please try again later.",
    "type": "rate_limit_error",
    "code": "rate_limit_exceeded"
  }
}
```

**Resolution:** Implement exponential backoff and retry logic. Check the `Retry-After` header for when to retry.

### [Insufficient Points (402)](https://creator.poe.com/api-reference/errors\#insufficient-points-402)

```
{
  "error": {
    "message": "Insufficient points to complete this request",
    "type": "insufficient_quota",
    "code": "insufficient_points"
  }
}
```

**Resolution:** Check your balance with [Get Current Balance](https://creator.poe.com/api-reference/getCurrentBalance) and add more points to your account.

### [Server Errors (500, 503)](https://creator.poe.com/api-reference/errors\#server-errors-500-503)

```
{
  "error": {
    "message": "An unexpected error occurred. Please try again.",
    "type": "api_error",
    "code": "internal_error"
  }
}
```

**Resolution:** These are temporary issues. Implement retry logic with exponential backoff.

## [Error Handling Best Practices](https://creator.poe.com/api-reference/errors\#error-handling-best-practices)

### [1\. Always Check Status Codes](https://creator.poe.com/api-reference/errors\#1-always-check-status-codes)

```
import requests

response = requests.post(
    'https://api.poe.com/v1/chat/completions',
    headers={'Authorization': f'Bearer {api_key}'},
    json={'model': 'GPT-4', 'messages': messages}
)

if response.status_code != 200:
    error = response.json()['error']
    print(f"Error {response.status_code}: {error['message']}")
    # Handle error appropriately
else:
    data = response.json()
    # Process successful response
```

### [2\. Implement Retry Logic](https://creator.poe.com/api-reference/errors\#2-implement-retry-logic)

For transient errors (429, 500, 503), implement exponential backoff:

```
import time
import requests

def make_request_with_retry(url, headers, data, max_retries=3):
    for attempt in range(max_retries):
        response = requests.post(url, headers=headers, json=data)

        if response.status_code == 200:
            return response.json()

        if response.status_code in [429, 500, 503]:
            wait_time = 2 ** attempt  # Exponential backoff
            print(f"Retrying in {wait_time} seconds...")
            time.sleep(wait_time)
        else:
            # Non-retryable error
            raise Exception(f"API Error: {response.json()}")

    raise Exception("Max retries exceeded")
```

### [3\. Handle Streaming Errors](https://creator.poe.com/api-reference/errors\#3-handle-streaming-errors)

When using streaming responses, errors can occur mid-stream:

```
import requests

response = requests.post(
    'https://api.poe.com/v1/chat/completions',
    headers={'Authorization': f'Bearer {api_key}'},
    json={'model': 'GPT-4', 'messages': messages, 'stream': True},
    stream=True
)

if response.status_code != 200:
    error = response.json()['error']
    print(f"Error: {error['message']}")
else:
    try:
        for line in response.iter_lines():
            if line:
                # Process streaming data
                data = json.loads(line.decode('utf-8').removeprefix('data: '))
                print(data)
    except Exception as e:
        print(f"Streaming error: {e}")
```

### [4\. Validate Before Sending](https://creator.poe.com/api-reference/errors\#4-validate-before-sending)

Reduce errors by validating input before making requests:

```
def validate_request(model, messages):
    # Check model exists
    valid_models = ['GPT-4', 'Claude-3-Opus', 'Gemini-Pro']
    if model not in valid_models:
        raise ValueError(f"Invalid model: {model}")

    # Check messages format
    if not messages or not isinstance(messages, list):
        raise ValueError("Messages must be a non-empty list")

    for msg in messages:
        if 'role' not in msg or 'content' not in msg:
            raise ValueError("Each message must have 'role' and 'content'")

    return True
```

### [5\. Log Errors for Debugging](https://creator.poe.com/api-reference/errors\#5-log-errors-for-debugging)

Keep detailed logs of errors for troubleshooting:

```
import logging

logging.basicConfig(level=logging.INFO)
logger = logging.getLogger(__name__)

try:
    response = client.create_chat_completion(model='GPT-4', messages=messages)
except Exception as e:
    logger.error(f"API request failed: {e}", extra={
        'model': 'GPT-4',
        'messages': messages,
        'timestamp': time.time()
    })
    raise
```

## [Rate Limiting](https://creator.poe.com/api-reference/errors\#rate-limiting)

The Poe API implements rate limiting to ensure fair usage. When you exceed rate limits:

- You'll receive a `429` status code
- The `Retry-After` header indicates how long to wait (in seconds)
- Your request won't be processed or consume points

**Best Practices:**

- Implement request queuing to avoid bursts
- Respect the `Retry-After` header
- Monitor your request rate
- Consider upgrading your plan if you frequently hit limits

## [Monitoring and Debugging](https://creator.poe.com/api-reference/errors\#monitoring-and-debugging)

### [Check Your Balance Regularly](https://creator.poe.com/api-reference/errors\#check-your-balance-regularly)

```
curl https://api.poe.com/v1/balance \
  -H "Authorization: Bearer YOUR_API_KEY"
```

### [Review Usage History](https://creator.poe.com/api-reference/errors\#review-usage-history)

```
curl https://api.poe.com/v1/usage/history \
  -H "Authorization: Bearer YOUR_API_KEY"
```

### [Test with Small Requests](https://creator.poe.com/api-reference/errors\#test-with-small-requests)

When debugging, start with minimal requests to isolate issues:

```
{
  "model": "GPT-4",
  "messages": [\
    {"role": "user", "content": "test"}\
  ],
  "max_tokens": 10
}
```

## [Getting Help](https://creator.poe.com/api-reference/errors\#getting-help)

If you encounter persistent errors:

1. Reach out to [developers@poe.com](mailto:developers@poe.com)
2. Review this documentation and the endpoint-specific guides
3. Verify your API key and account status
4. Contact support with error details and request IDs

## [Next Steps](https://creator.poe.com/api-reference/errors\#next-steps)

- [Learn about authentication](https://creator.poe.com/api-reference/overview#authentication)
- [Explore available models](https://creator.poe.com/api-reference/listModels)
- [Create chat completions](https://creator.poe.com/api-reference/createChatCompletion)
- [Monitor your usage](https://creator.poe.com/api-reference/getCurrentBalance)