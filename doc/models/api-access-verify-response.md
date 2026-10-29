
# Api Access Verify Response

Whether the code is valid.

## Structure

`ApiAccessVerifyResponse`

## Fields

| Name | Type | Tags | Description |
|  --- | --- | --- | --- |
| `valid` | `bool` | Required | True if the code belongs to a paid, unrefunded order for this shop. |
| `product` | `str` | Optional | The product name, when valid. |

## Example

```python
from onethingapi.models.api_access_verify_response import ApiAccessVerifyResponse

api_access_verify_response = ApiAccessVerifyResponse(
    valid=True,
    product='Vintage Cream and Red Roller Skates'
)
```

