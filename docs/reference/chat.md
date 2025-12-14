# Chat

## Create chat completion

**HTTP**: `POST https://api.poe.com/v1/chat/completions`

### Method

```python
def create(
    self,
    *,
    model: str,
    messages: list[dict],
    max_tokens: int | None = None,
    max_completion_tokens: int | None = None,
    temperature: float | None = None,
    top_p: float | None = None,
    stop: str | list[str] | None = None,
    stream: bool = False,
    stream_options: dict | None = None,
    tools: list[dict] | None = None,
    tool_choice: str | dict | None = None,
    parallel_tool_calls: bool | None = None,
    n: int = 1,
    extra_headers: dict[str, str] | None = None,
    extra_body: dict | None = None,
) -> ChatCompletion | "Iterator[ChatCompletionChunk]":
    ...
```

### Parameters

- **`model`** (`str`, required)
  - Poe model/bot ID (e.g. `Claude-Sonnet-4`).
- **`messages`** (`list[dict]`, required)
  - Each message has `role` and `content`.
- **`stream`** (`bool`, optional)
  - If `True`, yields streaming chunks and ends with a `[DONE]` event.
- **`max_tokens` / `max_completion_tokens`** (`int | None`)
- **`temperature`** (`float | None`)
  - Supported range: 0–2.
- **`top_p`** (`float | None`)
  - Supported range: 0–1.
- **`stop`** (`str | list[str] | None`)
  - Up to 4 stop sequences.
- **`tools`** (`list[dict] | None`)
  - OpenAI tools schema.
- **`tool_choice`** (`str | dict | None`)
- **`parallel_tool_calls`** (`bool | None`)
- **`n`** (`int`)
  - Must be exactly `1` (documented).
- **`extra_headers`** (`dict[str, str] | None`)
  - Per-request headers, e.g. `HTTP-Referer`, `X-Title`.
- **`extra_body`** (`dict | None`)
  - For OpenAI-compatibility scenarios, used to pass bot-specific parameters.

### Returns

- If `stream=False`: a `ChatCompletion` object.
- If `stream=True`: an iterator of `ChatCompletionChunk` objects.

### Response shape (non-streaming)

A typical response includes:

- `id: str`
- `object: "chat.completion"`
- `created: int` (unix seconds)
- `model: str`
- `choices: list[...]` (always length 1)
- `usage.prompt_tokens`, `usage.completion_tokens`, `usage.total_tokens`

### Response shape (streaming)

Streaming yields events with:

- `object: "chat.completion.chunk"`
- `choices[0].delta.content` providing incremental tokens

### Notes

- Private bots are not supported.
- For image/video/audio generation bots, use `stream=False`.
- Many unsupported OpenAI fields are silently ignored.

## Best Practices

### Streaming vs Non-Streaming

- **Text models**: Use `stream=True` for better user experience (lower perceived latency).
- **Media models**: Use `stream=False` for image/video/audio generation bots, as they typically return complete outputs and streaming may not work as expected.

### Error Handling

- Implement retry logic with exponential backoff for rate limits (`429`) and temporary server errors (`503`).
- Monitor the `X-RateLimit-Remaining` header.
