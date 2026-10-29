
# Shop Photos

The shop's photos.

## Structure

`ShopPhotos`

## Fields

| Name | Type | Tags | Description |
|  --- | --- | --- | --- |
| `photos` | [`List[Photo]`](../../doc/models/photo.md) | Required | Every photo, the cover first. |

## Example

```python
from onethingapi.models.photo import Photo
from onethingapi.models.shop_photos import ShopPhotos

shop_photos = ShopPhotos(
    photos=[
        Photo(
            id='LFRvGuTU3D8i334X',
            url='/api/blobs/LFRvGuTU3D8i334X'
        )
    ]
)
```

