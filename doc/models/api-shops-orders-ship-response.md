
# Api Shops Orders Ship Response

The order is marked shipped.

## Structure

`ApiShopsOrdersShipResponse`

## Fields

| Name | Type | Tags | Description |
|  --- | --- | --- | --- |
| `ok` | `bool` | Required | Always `true`. |
| `synced` | `bool` | Required | Whether PayPal accepted the tracking number. |

## Example

```python
from onethingapi.models.api_shops_orders_ship_response import ApiShopsOrdersShipResponse

api_shops_orders_ship_response = ApiShopsOrdersShipResponse(
    ok=True,
    synced=True
)
```

