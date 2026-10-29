
# Api Shops Color Photos Response

The colours that changed.

## Structure

`ApiShopsColorPhotosResponse`

## Fields

| Name | Type | Tags | Description |
|  --- | --- | --- | --- |
| `saved` | `List[str]` | Required | Colour labels whose photo changed. |

## Example

```python
from onethingapi.models.api_shops_color_photos_response import ApiShopsColorPhotosResponse

api_shops_color_photos_response = ApiShopsColorPhotosResponse(
    saved=[
        'Ice Blue',
        'Amber'
    ]
)
```

