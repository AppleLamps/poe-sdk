# Models

## List models

**HTTP**: `GET https://api.poe.com/v1/models`

### Method

```python
def list(
    self,
    *,
    extra_headers: dict[str, str] | None = None,
) -> ModelList:
    ...
```

### Authentication

The docs note this endpoint does **not** require authentication and returns publicly available models.

### Returns

`ModelList` with:

- `object: "list"`
- `data: list[Model]`

Each `Model` can include:

- `id: str`
- `object: "model"`
- `created: int` (unix ms)
- `description: str | None`
- `owned_by: str`
- `architecture`:
  - `input_modalities: list[str]`
  - `output_modalities: list[str]`
  - `modality: str`
- `pricing`:
  - `prompt: str | None`
  - `completion: str | None`
  - `image: str | None`
  - `request: str | None`

### Best Practices

- **Caching**: Model availability doesn't change frequently. Cache the response for 1-24 hours.
- **Filtering**: Filter by `architecture.input_modalities` for your use case.
- **Pricing**: Use the `pricing` field to estimate costs.
  - `prompt`: Cost per prompt token.
  - `completion`: Cost per completion token.
  - `image`: Cost per generated image.
  - `request`: Cost per request.

### Errors

- `429 rate_limit_error` (500 rpm)
