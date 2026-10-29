
# Api Shops Refine Request

The design change, in words.

## Structure

`ApiShopsRefineRequest`

## Fields

| Name | Type | Tags | Description |
|  --- | --- | --- | --- |
| `instruction` | `str` | Required | What to change, e.g. "make it feel more premium".<br><br>**Constraints**: *Maximum Length*: `500` |

## Example

```python
from onethingapi.models.api_shops_refine_request import ApiShopsRefineRequest

api_shops_refine_request = ApiShopsRefineRequest(
    instruction='Make it feel more premium'
)
```

