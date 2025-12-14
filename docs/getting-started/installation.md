# Installation

## Primary: poe-sdk

Install the package via pip:

```bash
pip install poe-sdk
```

## Alternatives: Official Provider SDKs

Since the Poe API is compatible with OpenAI and Anthropic specifications, you can also use their official SDKs if you prefer.

### OpenAI SDK

```bash
pip install openai
# or
npm install openai
```

### Anthropic SDK

```bash
pip install anthropic
# or
npm install @anthropic-ai/sdk
```

## Environment Setup

We recommend using `python-dotenv` to manage your keys.

```bash
pip install python-dotenv
```

```python
from dotenv import load_dotenv
load_dotenv()
```
