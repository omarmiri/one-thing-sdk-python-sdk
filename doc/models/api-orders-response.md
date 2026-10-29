
# Api Orders Response

The PayPal order to approve.

## Structure

`ApiOrdersResponse`

## Fields

| Name | Type | Tags | Description |
|  --- | --- | --- | --- |
| `id` | `str` | Required | PayPal order id. |

## Example

```python
from onethingapi.models.api_orders_response import ApiOrdersResponse

api_orders_response = ApiOrdersResponse(
    id='5O190127TN364715T'
)
```

