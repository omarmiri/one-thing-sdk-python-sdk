
# Shipping

Shipping cost and destinations.

## Structure

`Shipping`

## Fields

| Name | Type | Tags | Description |
|  --- | --- | --- | --- |
| `amount` | `float` | Required | Shipping cost per order. |
| `currency` | `str` | Required | ISO 4217 currency code. |
| `ships_to` | `List[str]` | Required | Country codes; empty means anywhere PayPal ships. |

## Example

```python
from onethingapi.models.shipping import Shipping

shipping = Shipping(
    amount=15,
    currency='USD',
    ships_to=[
        'US',
        'CA'
    ]
)
```

