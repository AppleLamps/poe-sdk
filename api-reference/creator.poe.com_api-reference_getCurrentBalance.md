---
url: "https://creator.poe.com/api-reference/getCurrentBalance"
title: "Get current point balance | Poe Creator Platform"
---

# Get current point balance

GET`https://api.poe.com/usage/current_balance`

Code example

Check remaining Poe API points for your organization.

cURL

cURL

```
curl https://api.poe.com/usage/current_balance \
-H "Authorization: Bearer sk_test_51SAMPLEKEY" \
-H "Accept: application/json"
```

Example balance

```json
{
"current_point_balance": 295932027
}
```

## [Overview](https://creator.poe.com/api-reference/getCurrentBalance\#overview)

Retrieve your current point balance, including both plan points and add-on points.

Use this endpoint to monitor your available points before making API calls.

## [Authentication](https://creator.poe.com/api-reference/getCurrentBalance\#authentication)

Send your Poe API key in the `Authorization` header:

```
Authorization: Bearer sk_test_51SAMPLEKEY
```

All requests must be made over HTTPS.

## [Parameters](https://creator.poe.com/api-reference/getCurrentBalance\#parameters)

This endpoint does not accept query or path parameters.

## [Responses](https://creator.poe.com/api-reference/getCurrentBalance\#responses)

| Field | Type | Required | Description |
| --- | --- | --- | --- |
| `current_point_balance` | integer | **Required** | Your current available points |

## [❌ Error codes](https://creator.poe.com/api-reference/getCurrentBalance\#-error-codes)

| Http | Type | Description |
| --- | --- | --- |
| 401 | `authentication_error` | Authentication failed Invalid API key |

## [Best Practices](https://creator.poe.com/api-reference/getCurrentBalance\#best-practices)

Check your balance before making expensive API calls. If balance is insufficient, requests will fail with 402 status.

Monitor your point balance to avoid service interruptions:

- Check balance before batch operations
- Set up alerts when balance drops below threshold
- Monitor usage patterns via `/usage/points_history`

## [🔁 Callbacks & webhooks](https://creator.poe.com/api-reference/getCurrentBalance\#-callbacks--webhooks)

No callbacks or webhooks are associated with this endpoint.

Code example

Check remaining Poe API points for your organization.

cURL

cURL

```
curl https://api.poe.com/usage/current_balance \
-H "Authorization: Bearer sk_test_51SAMPLEKEY" \
-H "Accept: application/json"
```

Example balance

```json
{
"current_point_balance": 295932027
}
```