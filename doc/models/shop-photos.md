
# Shop Photos

## Structure

`ShopPhotos`

## Fields

| Name | Type | Tags | Description |
|  --- | --- | --- | --- |
| `photos` | [`List[Photo]`](../../doc/models/photo.md) | Required | - |

## Example

```python
from onethingapi.models.photo import Photo
from onethingapi.models.shop_photos import ShopPhotos

shop_photos = ShopPhotos(
    photos=[
        Photo(
            id='id8',
            url='url2'
        )
    ]
)
```

