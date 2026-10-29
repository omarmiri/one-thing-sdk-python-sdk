
# Api Channel 3 Search Response

## Structure

`ApiChannel3SearchResponse`

## Fields

| Name | Type | Tags | Description |
|  --- | --- | --- | --- |
| `products` | [`List[ProductCard]`](../../doc/models/product-card.md) | Required | - |

## Example

```python
from onethingapi.models.api_channel_3_search_response import ApiChannel3SearchResponse
from onethingapi.models.product_card import ProductCard

api_channel_3_search_response = ApiChannel3SearchResponse(
    products=[
        ProductCard(
            id='id2',
            title='title2',
            image='image4',
            price=194.6,
            currency='currency8',
            retailer='retailer8',
            retailers=28,
            commission=62.94,
            brand='brand6'
        )
    ]
)
```

