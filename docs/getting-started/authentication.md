# Authentication

All authenticated Poe API calls use a Poe **API key**.

## Get an API key

- Create/copy your key at `https://poe.com/api_key`

## Recommended: environment variables

PowerShell (current session):

```powershell
$env:POE_API_KEY = "your_api_key_here"
```

PowerShell (persist user-level):

```powershell
[System.Environment]::SetEnvironmentVariable('POE_API_KEY', 'your_api_key_here', 'User')
```

In Python:

```python
import os
api_key = os.environ["POE_API_KEY"]
```

## HTTP header

Poe uses a bearer token header:

```text
Authorization: Bearer <POE_API_KEY>
```

## Security best practices

**⚠️ Security Warning**: Your API key provides full access to your Poe account and point balance.

- **Do NOT** commit keys to version control (git).
- **Do NOT** expose keys in client-side code (browsers, mobile apps).
- **Use environment variables** for all key management.
- **Rotate keys periodically** and revoke compromised keys immediately at [poe.com/api_key](https://poe.com/api_key).
- Use separate keys for development and production environments.

## Optional: leaderboard attribution headers

If you want Poe to attribute requests to your external application (leaderboard):

- `HTTP-Referer`: URL associated with your app
- `X-Title`: display name

These can be configured as default headers in the client or passed per-request.
