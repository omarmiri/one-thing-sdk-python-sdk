
# Api Shops Color Photos Request

## Structure

`ApiShopsColorPhotosRequest`

## Fields

| Name | Type | Tags | Description |
|  --- | --- | --- | --- |
| `photos` | `Dict[str, str]` | Required | Colour label → photo id, or `null`. |

## Example

```python
from onethingapi.models.api_shops_color_photos_request import ApiShopsColorPhotosRequest

api_shops_color_photos_request = ApiShopsColorPhotosRequest(
    photos={
        'key0': 'photos4'
    }
)
```

