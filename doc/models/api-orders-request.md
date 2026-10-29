
# Api Orders Request

## Structure

`ApiOrdersRequest`

## Fields

| Name | Type | Tags | Description |
|  --- | --- | --- | --- |
| `slug` | `str` | Required | - |
| `options` | `Dict[str, str]` | Optional | The buyer's pick, one value per option, keyed by option name. |

## Example

```python
from onethingapi.models.api_orders_request import ApiOrdersRequest

api_orders_request = ApiOrdersRequest(
    slug='slug0',
    options={
        'Size': 'M',
        'Color': 'Black'
    }
)
```

