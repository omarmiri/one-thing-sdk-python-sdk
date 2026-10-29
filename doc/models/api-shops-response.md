
# Api Shops Response

The shop was saved.

## Structure

`ApiShopsResponse`

## Fields

| Name | Type | Tags | Description |
|  --- | --- | --- | --- |
| `ok` | `bool` | Required | Always `true`. |
| `slug` | `str` | Required | The shop's link name after this change. |

## Example

```python
from onethingapi.models.api_shops_response import ApiShopsResponse

api_shops_response = ApiShopsResponse(
    ok=True,
    slug='vintageskates'
)
```

