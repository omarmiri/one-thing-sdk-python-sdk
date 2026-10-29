
# Api Shops Orders Refund Response

The refund.

## Structure

`ApiShopsOrdersRefundResponse`

## Fields

| Name | Type | Tags | Description |
|  --- | --- | --- | --- |
| `ok` | `bool` | Required | Always `true`. |
| `refund_id` | `str` | Optional | PayPal's refund id; null when `record` was used. |

## Example

```python
from onethingapi.models.api_shops_orders_refund_response import ApiShopsOrdersRefundResponse

api_shops_orders_refund_response = ApiShopsOrdersRefundResponse(
    ok=True,
    refund_id='1JU08902781691411'
)
```

