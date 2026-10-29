
# Json Rpc Request

## Structure

`JsonRpcRequest`

## Fields

| Name | Type | Tags | Description |
|  --- | --- | --- | --- |
| `jsonrpc` | `str` | Required, Constant | **Value**: `"2.0"` |
| `id` | str \| int \| None | Optional | This is a container for one-of cases. |
| `method` | [`Method`](../../doc/models/method.md) | Required | - |
| `params` | `Any` | Optional | For `tools/call`: `{ name, arguments }`. |

## Example

```python
import jsonpickle

from onethingapi.models.json_rpc_request import JsonRpcRequest
from onethingapi.models.method import Method

json_rpc_request = JsonRpcRequest(
    method=Method.PING,
    id='String1',
    params=jsonpickle.decode('{"key1":"val1","key2":"val2"}')
)
```

