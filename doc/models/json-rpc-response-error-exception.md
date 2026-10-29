
# Json Rpc Response Error Exception

A JSON-RPC 2.0 reply from the MCP server.

## Structure

`JsonRpcResponseErrorException`

## Fields

| Name | Type | Tags | Description |
|  --- | --- | --- | --- |
| `jsonrpc` | `str` | Required, Constant | Always `2.0`.<br><br>**Value**: `"2.0"` |
| `id` | str \| int \| None | Required | This is a container for one-of cases. |
| `result` | `Any` | Optional | For `tools/call`: `content` (the answer as JSON text), `structuredContent` (the same object) and `isError`. |
| `error` | [`Error`](../../doc/models/error.md) | Optional | Present when the call failed. |

## Example

```python
try:
    # make the API call
except JsonRpcResponseErrorException as e:
    print(e)
except ApiException as e:
    print(e)
```

