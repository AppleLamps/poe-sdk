# Chat Completions

Poe’s primary API is OpenAI-compatible chat completions.

## Endpoint

- `POST https://api.poe.com/v1/chat/completions`

## Non-streaming example

```python
import os
from poe_sdk import PoeClient

client = PoeClient(api_key=os.environ["POE_API_KEY"])

resp = client.chat.completions.create(
    model="Claude-Sonnet-4",
    messages=[{"role": "user", "content": "Top 3 things to do in NYC?"}],
)

print(resp.choices[0].message.content)
```

## Streaming example

When `stream=True`, the API returns chunks until a terminal `[DONE]` event.

```python
import os
from poe_sdk import PoeClient

client = PoeClient(api_key=os.environ["POE_API_KEY"])

stream = client.chat.completions.create(
    model="Claude-Sonnet-4",
    messages=[
        {"role": "system", "content": "You are a helpful travel agent."},
        {"role": "user", "content": "Tell me about San Francisco"},
    ],
    stream=True,
)

for chunk in stream:
    delta = chunk.choices[0].delta
    if delta and delta.content:
        print(delta.content, end="", flush=True)
```

## Multi-modal inputs

`messages[].content` can be a list of blocks instead of a string.

### Image/File input via data URL

Poe supports various file types via base64-encoded data URLs:

- **Images**: `image/jpeg`, `image/png`, etc.
- **Documents**: `application/pdf`, `text/plain`, etc.
- **Audio/Video**: `audio/mp3`, `video/mp4`, etc.

```python
import base64
import os
from poe_sdk import PoeClient

client = PoeClient(api_key=os.environ["POE_API_KEY"])

def encode_file(path):
    with open(path, "rb") as f:
        return base64.b64encode(f.read()).decode("utf-8")

pdf_b64 = encode_file("doc.pdf")

resp = client.chat.completions.create(
    model="Claude-Sonnet-4",
    messages=[{
        "role": "user",
        "content": [
            {"type": "text", "text": "Summarize this document."},
            {
                "type": "file",
                "file": {
                    "filename": "doc.pdf",
                    "file_data": f"data:application/pdf;base64,{pdf_b64}"
                }
            },
        ],
    }],
)
```

## Custom Parameters

You can pass bot-specific parameters (like `thinking_budget` or `reasoning_effort`) using `extra_body`.

```python
resp = client.chat.completions.create(
    model="Claude-Sonnet-4.5",
    messages=[{"role": "user", "content": "Explain quantum physics."}],
    extra_body={
        "thinking_budget": 1024,  # For Claude 3.7+
        # "reasoning_effort": "high",  # For o1/o3 models
        # "aspect_ratio": "16:9",      # For image models
    }
)
```

## Common parameters

- `max_tokens`, `max_completion_tokens`
- `temperature` (0–2)
- `top_p` (0–1)
- `stop` (string or list)
- `tools`, `tool_choice`, `parallel_tool_calls` (tool calling)
- `stream`, `stream_options`

## Notes and limitations (documented)

- **Private bots are not currently supported.**
- For **image/video/audio bots**, prefer `stream=False`.
- `n` must be exactly `1`.
- Unsupported fields are often ignored rather than erroring.
