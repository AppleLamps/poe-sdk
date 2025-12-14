# Anthropic Compatibility

Poe provides an Anthropic-compatible interface for accessing Claude models.

## Base URL

Set the Anthropic client base URL to:

- `https://api.poe.com`

## Endpoint

- `POST /v1/messages`

## Usage

### Python (Anthropic SDK)

```python
import os
import anthropic

client = anthropic.Anthropic(
    api_key=os.getenv("POE_API_KEY"),
    base_url="https://api.poe.com",
)

message = client.messages.create(
    model="claude-sonnet-4",
    max_tokens=1024,
    messages=[{"role": "user", "content": "Hello world"}],
)
print(message.content[0].text)
```

### Authentication

The API supports two methods:

1. **`x-api-key` header** (Recommended, standard Anthropic method)
2. **`Authorization: Bearer` header** (For compatibility)

## Supported Models

You can use any Claude model available on Poe. Examples:

- `Claude-Sonnet-4.5` (`claude-sonnet-4.5`)
- `Claude-Opus-4.5` (`claude-opus-4.5`)
- `Claude-Haiku-4.5` (`claude-haiku-4.5`)
- `Claude-Opus-4.1` (`claude-opus-4.1`)
- `Claude-Sonnet-4` (`claude-sonnet-4`)

## Rate Limits

- **500 requests per minute (RPM)**.
- Responses include standard rate limit headers.

## Differences from other APIs

- Only official Anthropic bots are supported. Custom bots or bots from other providers (like GPT-4) cannot be called via this endpoint.
