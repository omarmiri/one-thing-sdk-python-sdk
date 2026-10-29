
# Call Mcp Response

## Data Type

`JsonRpcResponse | List[JsonRpcResponse]`

## Cases

| Type |
|  --- |
| [`JsonRpcResponse`](../../../doc/models/json-rpc-response.md) |
| [`List[JsonRpcResponse]`](../../../doc/models/json-rpc-response.md) |

## JsonRpcResponse

### Initialization Code

#### Example

```python
value = JsonRpcResponse(
    id=1,
    result=jsonpickle.decode('{"content":[{"type":"text","text":"{\\"shop\\": \\"vintageskates\\"}"}],"isError":false}')
)
```

## List[JsonRpcResponse]

### Initialization Code

#### Example

```python
value = [
    JsonRpcResponse(
        id=1,
        result=jsonpickle.decode('{"content":[{"type":"text","text":"{\\"shop\\": \\"vintageskates\\"}"}],"isError":false}')
    )
]
```

