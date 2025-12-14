# Tool Calling

Tool calling (function calling) lets a model propose structured tool invocations. Your application executes them and returns results back to the model.

## How it works

1. You send a request with `tools` defined.
2. The model may respond with `tool_calls`.
3. Your client executes each tool call.
4. You append tool outputs as messages with `role="tool"`.
5. You send a follow-up request (with the updated conversation) to get the final answer.

## Define tools

Tools follow the OpenAI tools schema.

```python
TOOLS = [
    {
        "type": "function",
        "function": {
            "name": "plus",
            "description": "Add two integers together",
            "parameters": {
                "type": "object",
                "properties": {
                    "a": {"type": "integer", "description": "First integer"},
                    "b": {"type": "integer", "description": "Second integer"},
                },
                "required": ["a", "b"],
            },
        },
    }
]
```

## Full example

```python
import json
import os
from poe_sdk import PoeClient

client = PoeClient(api_key=os.environ["POE_API_KEY"])

messages = [
    {"role": "user", "content": "What is 1999 + 2036?"}
]

first = client.chat.completions.create(
    model="GPT-5",
    messages=messages,
    tools=TOOLS,
    tool_choice="auto",
)

assistant = first.choices[0].message

# If there are no tool calls, you're done
if not getattr(assistant, "tool_calls", None):
    print(assistant.content)
else:
    tool_messages = []
    for tool_call in assistant.tool_calls:
        if tool_call.function.name == "plus":
            args = json.loads(tool_call.function.arguments)
            result = args["a"] + args["b"]
            tool_messages.append({
                "role": "tool",
                "tool_call_id": tool_call.id,
                "content": str(result),
            })

    messages.append(assistant)
    messages.extend(tool_messages)

    final = client.chat.completions.create(
        model="GPT-5",
        messages=messages,
        tools=TOOLS,
    )

    print(final.choices[0].message.content)
```

## Agentic Loop

The model can iterate through multiple tool calls, reasoning about intermediate results. Here is a conceptual pattern for an agentic loop:

1. **Initial Request**: Send user message with tools.
2. **Loop**:
   - Check if response contains `tool_calls`.
   - If no tool calls -> **Break** (final answer reached).
   - Execute each tool call.
   - Append tool results to messages list.
   - Send new request with updated messages.
   - Repeat.

This enables iterative reasoning and complex multi-step workflows.

## Compatibility note

The docs note that some OpenAI tool-calling options may not work with all Poe models (even if they are valid OpenAI parameters). For example, `tool_choice` with `allowed_tools` is only supported by some models.

Also, `strict` tool calling is ignored, so tool arguments are not guaranteed to conform to schemas.
