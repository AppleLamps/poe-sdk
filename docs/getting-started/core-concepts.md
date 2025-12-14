# Core Concepts

## Models and bots

In Poe’s OpenAI-compatible API, the request field is called `model`, but it expects a **Poe model/bot ID** (e.g. `Claude-Sonnet-4`, `GPT-5-Pro`, `Gemini-2.5-Pro`).

Important limitations (documented):

- **Private bots are not supported** via the API.
- The **App-Creator** bot is not available via API.

## Messages

Chat uses an OpenAI-style list of message objects:

- `role`: `system`, `user`, `assistant`, or `tool`
- `content`: typically a string; can also be a list of content blocks for multi-modal input

## Chat completions

The primary endpoint is:

- `POST https://api.poe.com/v1/chat/completions`

The response is OpenAI-compatible (`chat.completion`).

## Streaming

Set `stream=True` to receive incremental chunks (`chat.completion.chunk`) until a terminal `[DONE]` event.

Guidance (documented):

- Use `stream=True` for text chat UX.
- For image/video/audio generation bots, prefer `stream=False`.

## Tool calling

Tool calling (function calling) is supported using `tools` and `tool_choice`.

The model may return `tool_calls` in an assistant message. Your app executes tools and sends results back using messages with `role="tool"`.

## Points and billing

API usage consumes **points** from the account associated with the API key.

Usage endpoints:

- `GET https://api.poe.com/usage/current_balance`
- `GET https://api.poe.com/usage/points_history`
