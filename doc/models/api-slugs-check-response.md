
# Api Slugs Check Response

Whether the link name can be used.

## Structure

`ApiSlugsCheckResponse`

## Fields

| Name | Type | Tags | Description |
|  --- | --- | --- | --- |
| `slug` | `str` | Required | The name, normalised. |
| `available` | `bool` | Required | True if no other shop has it and it isn't reserved. |
| `problem` | `str` | Optional | Why not, when unavailable. |

## Example

```python
from onethingapi.models.api_slugs_check_response import ApiSlugsCheckResponse

api_slugs_check_response = ApiSlugsCheckResponse(
    slug='vintageskates',
    available=True,
    problem='Taken. Try another name.'
)
```

