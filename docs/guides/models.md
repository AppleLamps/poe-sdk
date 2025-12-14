# Models

Poe provides a unified model catalog across many providers.

## Endpoint

- `GET https://api.poe.com/v1/models`

The docs note this endpoint does not require authentication and returns publicly available models.

## Example

```python
from poe_sdk import PoeClient

client = PoeClient()
models = client.models.list()

for m in models.data[:20]:
    modality = None
    if getattr(m, "architecture", None):
        modality = m.architecture.modality
    print(m.id, m.owned_by, modality)
```

## Filtering suggestions

- Filter by `architecture.input_modalities` depending on your app.
- **Caching**: The list of available models changes infrequently. It is highly recommended to cache this response for **1-24 hours** to improve performance and reduce API calls.

## Pricing metadata

Each model may include `pricing` fields (strings) such as:

- `pricing.prompt`
- `pricing.completion`

Use these for rough estimation and display; your actual consumption is reflected in points usage history.
