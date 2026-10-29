
# Api Access Verify Request

The code to check, and which shop it's for.

## Structure

`ApiAccessVerifyRequest`

## Fields

| Name | Type | Tags | Description |
|  --- | --- | --- | --- |
| `shop` | `str` | Required | The shop's link name. |
| `code` | `str` | Required | The access code the buyer entered. Case and dashes don't matter. |

## Example

```python
from onethingapi.models.api_access_verify_request import ApiAccessVerifyRequest

api_access_verify_request = ApiAccessVerifyRequest(
    shop='raptorrush',
    code='K7QF-M2XP-9HTD'
)
```

