
# Api Slugs Check Response

## Structure

`ApiSlugsCheckResponse`

## Fields

| Name | Type | Tags | Description |
|  --- | --- | --- | --- |
| `slug` | `str` | Required | - |
| `available` | `bool` | Required | - |
| `problem` | `str` | Optional | Why not, when unavailable. |

## Example

```python
from onethingapi.models.api_slugs_check_response import ApiSlugsCheckResponse

api_slugs_check_response = ApiSlugsCheckResponse(
    slug='slug4',
    available=False,
    problem='problem2'
)
```

