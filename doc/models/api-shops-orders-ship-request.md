
# Api Shops Orders Ship Request

## Structure

`ApiShopsOrdersShipRequest`

## Fields

| Name | Type | Tags | Description |
|  --- | --- | --- | --- |
| `carrier` | [`Carrier`](../../doc/models/carrier.md) | Required | - |
| `carrier_name` | `str` | Optional | Required when `carrier` is `OTHER`.<br><br>**Constraints**: *Maximum Length*: `60` |
| `tracking_number` | `str` | Required | **Constraints**: *Minimum Length*: `4`, *Maximum Length*: `64` |

## Example

```python
from onethingapi.models.api_shops_orders_ship_request import ApiShopsOrdersShipRequest
from onethingapi.models.carrier import Carrier

api_shops_orders_ship_request = ApiShopsOrdersShipRequest(
    carrier=Carrier.DHL,
    tracking_number='trackingNumber4',
    carrier_name='carrierName6'
)
```

