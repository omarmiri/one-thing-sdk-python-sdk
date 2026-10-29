
# Offer 1

## Structure

`Offer1`

## Fields

| Name | Type | Tags | Description |
|  --- | --- | --- | --- |
| `retailer` | `str` | Required | - |
| `price` | `float` | Required | - |
| `currency` | `str` | Required | - |
| `in_stock` | `bool` | Required | - |
| `url` | `str` | Required | - |

## Example

```python
from onethingapi.models.offer_1 import Offer1

offer_1 = Offer1(
    retailer='retailer8',
    price=95,
    currency='currency2',
    in_stock=False,
    url='url6'
)
```

