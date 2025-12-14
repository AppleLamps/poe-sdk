# poe-sdk

Python SDK documentation for the Poe API.

## What is poe-sdk?

`poe-sdk` is a Python SDK for building applications that interact with **Poe.com** models and bots via the Poe API.

With the SDK you can:

- Send **chat completions** to Poe models/bots.
- **Stream** responses in real time.
- Use **tool calling** (function calling) to let models request structured tool invocations.
- **List models** and read modality/pricing metadata.
- Monitor **points balance** and **usage history**.

## Quickstart

```python
import os
from poe_sdk import PoeClient

client = PoeClient(api_key=os.environ["POE_API_KEY"])

resp = client.chat.completions.create(
    model="Claude-Sonnet-4",
    messages=[{"role": "user", "content": "Why is the sky blue?"}],
)

print(resp.choices[0].message.content)
```

## API endpoints (as documented)

- `POST https://api.poe.com/v1/chat/completions`
- `GET  https://api.poe.com/v1/models`
- `GET  https://api.poe.com/usage/current_balance`
- `GET  https://api.poe.com/usage/points_history`

## Next steps

- **Getting Started**
  - [Installation](getting-started/installation.md)
  - [Authentication](getting-started/authentication.md)
  - [Core Concepts](getting-started/core-concepts.md)

- **Guides**
  - [Chat Completions](guides/chat-completions.md)
  - [Tool Calling](guides/tool-calling.md)
  - [Integrations](guides/integrations.md) (Cursor, VS Code, etc.)

- **Advanced**
  - [Rate Limits](advanced/rate-limits.md)
  - [OpenAI Compatibility](advanced/openai-compat.md)
  - [Anthropic Compatibility](advanced/anthropic-compat.md)

- **Reference**
  - [Client](reference/client.md)
  - [Chat](reference/chat.md)
  - [Models](reference/models.md)
  - [Usage](reference/usage.md)
  - [Errors](reference/errors.md)
