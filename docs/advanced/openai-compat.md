# OpenAI Compatibility

Poe provides an OpenAI-compatible interface for Chat Completions.

## Base URL

Set the OpenAI client base URL to:

- `https://api.poe.com/v1`

The endpoint is:

- `POST /chat/completions`

## Key differences (documented)

- **Structured outputs are not supported** (e.g. `response_format` with `json_schema`).
- `strict` for tool calling is ignored.
- Audio input is ignored/stripped.
- Many unsupported fields are silently ignored.
- `n` must be exactly `1`.

## Known Issues & Limitations

- **Private bots**: Not currently supported.
- **Media bots**: Use `stream=False` for best results.
- **Parameter Handling**: Best-effort. Some model-specific parameters may not be supported.
- **Audio input**: Not supported; ignored.

## Detailed API Support

### Request fields

| Field | Support status |
| --- | --- |
| `model` | Use Poe bot names |
| `max_tokens` / `max_completion_tokens` | Fully supported |
| `stream` / `stream_options` | Fully supported |
| `tools` / `tool_choice` / `parallel_tool_calls` | Fully supported |
| `temperature` | 0-2 |
| `response_format` | Ignored |
| `audio` | Ignored |

### Response fields

| Field | Support status |
| --- | --- |
| `id`, `created`, `model` | Fully supported |
| `choices[].message` | Fully supported |
| `usage` | Fully supported |
| `logprobs` | Always empty |

## Custom parameters

When using the OpenAI SDK against Poe, pass bot-specific parameters using:

- `extra_body={...}`

Examples include `reasoning_effort`, `thinking_budget`, `aspect`, `quality`, etc.

## Migration checklist

1. Switch base URL: `https://api.openai.com/v1` → `https://api.poe.com/v1`
2. Replace environment variable: `OPENAI_API_KEY` → `POE_API_KEY`
3. Choose a Poe model ID (e.g. `Claude-Opus-4.1`)
4. Remove unsupported parameters (`n>1`, audio, etc.)
5. Run tests and validate outputs
