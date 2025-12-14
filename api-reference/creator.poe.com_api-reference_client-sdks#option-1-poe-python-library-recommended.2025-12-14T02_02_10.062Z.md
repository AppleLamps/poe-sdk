[![Poe Logo](https://creator.poe.com/_next/image?url=%2Fimg%2FpoeFullWhiteMultibot.svg&w=256&q=75)](https://creator.poe.com/)

[Docs](https://creator.poe.com/docs) [API Reference](https://creator.poe.com/api-reference) [Changelog](https://creator.poe.com/changelog) [Login](https://poe.com/login) [Sign up](https://poe.com/login)

Search`⌘`  `K`

Using the API

[Overview](https://creator.poe.com/api-reference/overview) [Client SDKs](https://creator.poe.com/api-reference/client-sdks) [Error Handling](https://creator.poe.com/api-reference/errors) [Rate Limits](https://creator.poe.com/api-reference/rate-limits)

Endpoints

[GETList available models](https://creator.poe.com/api-reference/listModels) [POSTCreate chat completion](https://creator.poe.com/api-reference/createChatCompletion) [GETGet current point balance](https://creator.poe.com/api-reference/getCurrentBalance) [GETGet usage history](https://creator.poe.com/api-reference/getPointsHistory)

# Client SDKs

The Poe API can be accessed through two primary methods: the native Poe Python library or the OpenAI-compatible REST API. Choose the method that best fits your use case.

## [Quick Comparison](https://creator.poe.com/api-reference/client-sdks\#quick-comparison)

| Feature | Poe Python Library | OpenAI-Compatible API |
| --- | --- | --- |
| **Installation** | `pip install fastapi-poe` | Any HTTP client or OpenAI SDK |
| **Language Support** | Python only | Any language (Python, Node.js, Go, cURL, etc.) |
| **Custom Parameters** | ✅ Full support | ❌ Not supported |
| **File Upload** | ✅ Native support | Limited |
| **Streaming** | ✅ Async/sync | ✅ Via standard streaming |
| **Error Handling** | ✅ Enhanced | Standard HTTP errors |
| **Best For** | New Python projects, custom parameters | OpenAI migrations, multi-language projects |

Recommendation

**For new Python projects:** Use the Poe Python library (`fastapi-poe`) for the best experience, native error handling, and full feature support including custom parameters.

**For OpenAI migration or non-Python projects:** Use the OpenAI-compatible API for seamless integration with existing tools.

* * *

## [Option 1: Poe Python Library (Recommended)](https://creator.poe.com/api-reference/client-sdks\#option-1-poe-python-library-recommended)

The official Poe Python library provides the most feature-complete way to interact with Poe bots and models.

### [Installation](https://creator.poe.com/api-reference/client-sdks\#installation)

```
pip install fastapi-poe
```

### [Basic Usage](https://creator.poe.com/api-reference/client-sdks\#basic-usage)

SynchronousAsynchronous

```
import fastapi_poe as fp

api_key = "your_api_key"  # Get from https://poe.com/api_key
message = fp.ProtocolMessage(role="user", content="Hello world")

for partial in fp.get_bot_response_sync(
    messages=[message],
    bot_name="GPT-3.5-Turbo",
    api_key=api_key
):
    print(partial)
```

```
import asyncio
import fastapi_poe as fp

async def get_response():
    api_key = "your_api_key"  # Get from https://poe.com/api_key
    message = fp.ProtocolMessage(role="user", content="Hello world")

    async for partial in fp.get_bot_response(
        messages=[message],
        bot_name="GPT-3.5-Turbo",
        api_key=api_key
    ):
        print(partial)

asyncio.run(get_response())
```

### [Key Features](https://creator.poe.com/api-reference/client-sdks\#key-features)

#### [Custom Parameters (Python Library Only)](https://creator.poe.com/api-reference/client-sdks\#custom-parameters-python-library-only)

The Poe Python library supports passing custom parameters that are not available via the OpenAI-compatible API:

Claude ModelsGPT ModelsImage Generation

```
import fastapi_poe as fp

message = fp.ProtocolMessage(
    role="user",
    content="Explain quantum computing",
    parameters={"thinking_budget": 1000}
)

for partial in fp.get_bot_response_sync(
    messages=[message],
    bot_name="Claude-Sonnet-4.5",
    api_key=api_key
):
    print(partial)
```

```
import fastapi_poe as fp

message = fp.ProtocolMessage(
    role="user",
    content="Solve this complex problem: ...",
    parameters={"reasoning_effort": "high"}
)

for partial in fp.get_bot_response_sync(
    messages=[message],
    bot_name="GPT-5",
    api_key=api_key
):
    print(partial)
```

```
import fastapi_poe as fp

message = fp.ProtocolMessage(
    role="user",
    content="A cat in a hat",
    parameters={
        "aspect_ratio": "9:16",
        "style": "photorealistic"
    }
)

for partial in fp.get_bot_response_sync(
    messages=[message],
    bot_name="Imagen-4",
    api_key=api_key
):
    print(partial)
```

Custom parameters like `thinking_budget`, `reasoning_effort`, and `aspect_ratio` **cannot be passed via the OpenAI-compatible API**. They must be passed through the `parameters` field in `ProtocolMessage` using the Poe Python library.

#### [File Upload](https://creator.poe.com/api-reference/client-sdks\#file-upload)

```
import fastapi_poe as fp

api_key = "your_api_key"

# Upload file
pdf_attachment = fp.upload_file_sync(
    open("document.pdf", "rb"),
    api_key=api_key
)

# Send message with attachment
message = fp.ProtocolMessage(
    role="user",
    content="Summarize this document",
    attachments=[pdf_attachment]
)

for partial in fp.get_bot_response_sync(
    messages=[message],
    bot_name="GPT-3.5-Turbo",
    api_key=api_key
):
    print(partial)
```

### [Available APIs](https://creator.poe.com/api-reference/client-sdks\#available-apis)

The Poe Python library can access:

- ✅ **Chat Completions** \- `fp.get_bot_response()` / `fp.get_bot_response_sync()`
- ✅ **File Upload** \- `fp.upload_file()` / `fp.upload_file_sync()`
- ✅ **Custom Parameters** \- Via `parameters` field
- ✅ **All public bots and models**

### [Learn More](https://creator.poe.com/api-reference/client-sdks\#learn-more)

For detailed documentation and advanced usage, see the [External Application Guide](https://creator.poe.com/docs/external-applications/external-application-guide).

* * *

## [Option 2: OpenAI-Compatible API](https://creator.poe.com/api-reference/client-sdks\#option-2-openai-compatible-api)

Use the standard OpenAI SDK or any HTTP client to access Poe models through an OpenAI-compatible interface.

### [Using the OpenAI SDK](https://creator.poe.com/api-reference/client-sdks\#using-the-openai-sdk)

PythonNode.jscURL

```
# pip install openai
import os
import openai

client = openai.OpenAI(
    api_key=os.getenv("POE_API_KEY"),  # https://poe.com/api_key
    base_url="https://api.poe.com/v1",
)

chat = client.chat.completions.create(
    model="Claude-Sonnet-4",
    messages=[{"role": "user", "content": "Top 3 things to do in NYC?"}],
)
print(chat.choices[0].message.content)
```

```
// npm install openai
import OpenAI from "openai";

const client = new OpenAI({
    apiKey: process.env.POE_API_KEY,  // https://poe.com/api_key
    baseURL: "https://api.poe.com/v1",
});

const completion = await client.chat.completions.create({
    model: "Claude-Sonnet-4",
    messages: [\
        {\
            role: "user",\
            content: "What are the top 3 things to do in New York?",\
        },\
    ],
});

console.log(completion.choices[0].message.content);
```

```
curl "https://api.poe.com/v1/chat/completions" \
    -H "Content-Type: application/json" \
    -H "Authorization: Bearer $POE_API_KEY" \
    -d '{
        "model": "Claude-Sonnet-4",
        "messages": [\
            {\
                "role": "user",\
                "content": "Write a one-sentence bedtime story."\
            }\
        ]
    }'
```

### [Using Raw HTTP Requests](https://creator.poe.com/api-reference/client-sdks\#using-raw-http-requests)

You can also make direct HTTP requests to the Poe API using any HTTP client:

Python requestsJavaScript fetchGoC#

```
import os
import requests

headers = {
    "Authorization": f"Bearer {os.environ['POE_API_KEY']}",
    "Content-Type": "application/json",
}

payload = {
    "model": "Claude-Sonnet-4",
    "messages": [\
        {"role": "user", "content": "What are the top 3 things to do in NYC?"}\
    ]
}

response = requests.post(
    "https://api.poe.com/v1/chat/completions",
    headers=headers,
    json=payload,
    timeout=30,
)

response.raise_for_status()
print(response.json())
```

```
const response = await fetch("https://api.poe.com/v1/chat/completions", {
    method: "POST",
    headers: {
        "Authorization": `Bearer ${process.env.POE_API_KEY}`,
        "Content-Type": "application/json",
    },
    body: JSON.stringify({
        model: "Claude-Sonnet-4",
        messages: [\
            { role: "user", content: "What are the top 3 things to do in NYC?" }\
        ]
    }),
});

const result = await response.json();
console.log(result);
```

```
package main

import (
    "bytes"
    "encoding/json"
    "fmt"
    "net/http"
    "os"
)

func main() {
    payload := map[string]any{
        "model": "Claude-Sonnet-4",
        "messages": []any{
            map[string]any{
                "role": "user",
                "content": "What are the top 3 things to do in NYC?",
            },
        },
    }

    body, _ := json.Marshal(payload)
    req, _ := http.NewRequest("POST", "https://api.poe.com/v1/chat/completions", bytes.NewReader(body))

    req.Header.Set("Authorization", "Bearer "+os.Getenv("POE_API_KEY"))
    req.Header.Set("Content-Type", "application/json")

    res, _ := http.DefaultClient.Do(req)
    defer res.Body.Close()

    var result map[string]any
    json.NewDecoder(res.Body).Decode(&result)
    fmt.Println(result)
}
```

```
using System;
using System.Net.Http;
using System.Net.Http.Json;

var http = new HttpClient();
http.DefaultRequestHeaders.Authorization =
    new System.Net.Http.Headers.AuthenticationHeaderValue(
        "Bearer",
        Environment.GetEnvironmentVariable("POE_API_KEY")
    );

var payload = new {
    model = "Claude-Sonnet-4",
    messages = new[] {
        new { role = "user", content = "What are the top 3 things to do in NYC?" }
    }
};

var response = await http.PostAsJsonAsync(
    "https://api.poe.com/v1/chat/completions",
    payload
);

var result = await response.Content.ReadFromJsonAsync<dynamic>();
Console.WriteLine(result);
```

### [Available APIs](https://creator.poe.com/api-reference/client-sdks\#available-apis-1)

The OpenAI-compatible API supports:

- ✅ **Chat Completions** \- `/v1/chat/completions` (streaming and non-streaming)
- ✅ **List Models** \- `/v1/models`
- ✅ **Current Balance** \- `/usage/current_balance`
- ✅ **Usage History** \- `/usage/points_history`
- ❌ **Custom Parameters** \- Not supported (use Poe Python library instead)

### [Key Limitations](https://creator.poe.com/api-reference/client-sdks\#key-limitations)

The OpenAI-compatible API has some limitations compared to the native Poe Python library:

- **No custom parameter support** \- Cannot pass `thinking_budget`, `reasoning_effort`, `aspect_ratio`, etc.
- **Private bots not supported** \- Only public bots can be accessed
- **App-Creator bot unavailable** \- Cannot be used via this API
- **Best-effort parameter passing** \- Some model-specific parameters may not work as expected
- **Media bots** \- Should be called with `stream=false` for best results

For detailed compatibility information, see the [OpenAI Compatible API Guide](https://creator.poe.com/docs/external-applications/openai-compatible-api).

* * *

## [Authentication](https://creator.poe.com/api-reference/client-sdks\#authentication)

All API methods require authentication using your Poe API key.

### [Get Your API Key](https://creator.poe.com/api-reference/client-sdks\#get-your-api-key)

1. Visit [https://poe.com/api\_key](https://poe.com/api_key)
2. Copy your API key
3. Store it securely (see best practices below)

### [Best Practices](https://creator.poe.com/api-reference/client-sdks\#best-practices)

Security Warning

Never expose your API key in client-side code, public repositories, or commit it to version control. Always keep it secure on your server or in environment variables.

**Key Management:**

- ✅ Store API keys in environment variables, not in code
- ✅ Use different API keys for development and production
- ✅ Rotate API keys periodically
- ✅ Revoke compromised keys immediately
- ❌ Never commit API keys to version control
- ❌ Never expose keys in client-side code

### [Environment Variable Setup](https://creator.poe.com/api-reference/client-sdks\#environment-variable-setup)

Bash/ZshPowerShellPython .envNode.js .env

```
# Add to ~/.bashrc or ~/.zshrc
export POE_API_KEY="your_api_key_here"

# Or set for current session
export POE_API_KEY="your_api_key_here"
```

```
# Set for current session
$env:POE_API_KEY = "your_api_key_here"

# Set permanently (user level)
[System.Environment]::SetEnvironmentVariable('POE_API_KEY', 'your_api_key_here', 'User')
```

```
# Create .env file
# POE_API_KEY=your_api_key_here

# Load in Python
from dotenv import load_dotenv
import os

load_dotenv()
api_key = os.getenv("POE_API_KEY")
```

```
// Create .env file
// POE_API_KEY=your_api_key_here

// Load in Node.js
import dotenv from 'dotenv';
dotenv.config();

const apiKey = process.env.POE_API_KEY;
```

* * *

## [Rate Limits and Usage](https://creator.poe.com/api-reference/client-sdks\#rate-limits-and-usage)

### [Rate Limits](https://creator.poe.com/api-reference/client-sdks\#rate-limits)

- **500 requests per minute** per API key
- Monitor usage with response headers
- Implement exponential backoff for retries

### [Point-Based Billing](https://creator.poe.com/api-reference/client-sdks\#point-based-billing)

All API usage consumes points from your account:

- Check balance: [Get Current Balance](https://creator.poe.com/api-reference/getCurrentBalance)
- View history: [Get Points History](https://creator.poe.com/api-reference/getPointsHistory)
- Purchase additional points: [https://poe.com/api\_key](https://poe.com/api_key)

Different models consume different amounts of points based on computational cost. See the [List Models](https://creator.poe.com/api-reference/listModels) endpoint for pricing information.
