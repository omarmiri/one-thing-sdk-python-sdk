
# Api Shops Refine Request

## Structure

`ApiShopsRefineRequest`

## Fields

| Name | Type | Tags | Description |
|  --- | --- | --- | --- |
| `instruction` | `str` | Required | **Constraints**: *Maximum Length*: `500` |

## Example

```python
from onethingapi.models.api_shops_refine_request import ApiShopsRefineRequest

api_shops_refine_request = ApiShopsRefineRequest(
    instruction='Make it feel more premium'
)
```

