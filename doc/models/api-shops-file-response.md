
# Api Shops File Response

## Structure

`ApiShopsFileResponse`

## Fields

| Name | Type | Tags | Description |
|  --- | --- | --- | --- |
| `ok` | `bool` | Required | - |
| `filename` | `str` | Required | - |

## Example

```python
from onethingapi.models.api_shops_file_response import ApiShopsFileResponse

api_shops_file_response = ApiShopsFileResponse(
    ok=False,
    filename='filename0'
)
```

