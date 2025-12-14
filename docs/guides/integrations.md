# Integrations

Poe's OpenAI-compatible API allows you to use your Poe subscription with popular AI coding tools.

## Prerequisites

- **Base URL**: `https://api.poe.com/v1/`
- **API Key**: [poe.com/api_key](https://poe.com/api_key)

## Cursor

1. Open **Settings** > **Models**.
2. Add a **Custom Model Provider** (OpenAI Compatible).
3. Configure:
   - **Base URL**: `https://api.poe.com/v1/`
   - **API Key**: Your Poe API Key
4. Add models like `Claude-Sonnet-4`, `GPT-4o`, `Gemini-2.5-Pro`.

## Cline (VS Code)

1. Open **Cline Settings**.
2. Select **OpenAI Compatible** as API Provider.
3. Configure:
   - **Base URL**: `https://api.poe.com/v1/`
   - **API Key**: Your Poe API Key
   - **Model ID**: e.g., `Claude-Sonnet-4`

## Roo Code

1. Open **Settings** > **Providers**.
2. Select **OpenAI Compatible**.
3. Configure:
   - **Base URL**: `https://api.poe.com/v1/`
   - **API Key**: Your Poe API Key
   - **Model**: e.g., `Claude-Sonnet-4`

## LLM (Command Line)

```bash
llm "Explain quantum computing" -m Claude-Sonnet-4 --api-base https://api.poe.com/v1 --key poe
```

## Troubleshooting

- **Invalid API Key**: Verify key at [poe.com/api_key](https://poe.com/api_key).
- **Model Not Found**: Use exact model names (e.g., `Claude-Sonnet-4`).
- **Connection Timeout**: Verify Base URL is `https://api.poe.com/v1/`.
