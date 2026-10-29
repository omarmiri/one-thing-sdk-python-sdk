
# Error

Present when the call failed.

## Structure

`Error`

## Fields

| Name | Type | Tags | Description |
|  --- | --- | --- | --- |
| `code` | `int` | Required | The JSON-RPC error code. |
| `message` | `str` | Required | What went wrong. |

## Example

```python
from onethingapi.models.error import Error

error = Error(
    code=-32601,
    message='Method not found'
)
```

