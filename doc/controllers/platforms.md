# Platforms

For marketplaces that make and run shops for their own sellers with one API key.

```python
platforms_api = client.platforms
```

## Class Name

`PlatformsApi`


# List My Shops

Every shop the API key's account owns, newest first, with what a catalog page needs: name, price, cover, link, whether PayPal is connected and how many sales it has.

```python
def list_my_shops(self,
                 status=None)
```

## Authentication

This endpoint requires [PlatformKey](../../doc/auth/oauth-2-bearer-token.md)

## Parameters

| Parameter | Type | Tags | Description |
|  --- | --- | --- | --- |
| `status` | [`Status`](../../doc/models/status.md) | Query, Optional | Only shops with this status, e.g. `live` for a public catalog. |

## Response Type

**200**: The shops.

[`ApiPlatformShopsResponse`](../../doc/models/api-platform-shops-response.md)

## Example Usage

```python
status = Status.LIVE

result = platforms_api.list_my_shops(
    status=status
)
print(result)
```

## Example Response *(as JSON)*

```json
{
  "shops": [
    {
      "slug": "raptorrush",
      "status": "live",
      "name": "Raptor Rush: Browser Edition",
      "headline": "Grow from Tiny Hatchling to Giant Apex Predator",
      "product_type": "digital",
      "price": {
        "amount": 2.99,
        "currency": "USD"
      },
      "url": "https://one-thing-ash0.onrender.com/raptorrush",
      "cover": "https://one-thing-ash0.onrender.com/api/blobs/KchAi9jwZzo76SKh",
      "paypal_connected": true,
      "sales": 12,
      "created_at": "2026-10-12T20:31:44Z"
    }
  ]
}
```

## Errors

| HTTP Status Code | Error Description | Exception Class |
|  --- | --- | --- |
| 401 | No API key, or it's wrong or revoked. | [`ErrorException`](../../doc/models/error-exception.md) |

