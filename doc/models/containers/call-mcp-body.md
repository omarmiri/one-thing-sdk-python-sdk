
# Call Mcp Body

## Data Type

`JsonRpcRequest | List[JsonRpcRequest]`

## Cases

| Type |
|  --- |
| [`JsonRpcRequest`](../../../doc/models/json-rpc-request.md) |
| [`List[JsonRpcRequest]`](../../../doc/models/json-rpc-request.md) |

## JsonRpcRequest

### Initialization Code

#### Example

```python
value = JsonRpcRequest(
    method=Method.ENUM_TOOLSCALL,
    id=1,
    params=jsonpickle.decode('{"name":"get_product","arguments":{"shop":"vintageskates"}}')
)
```

## List[JsonRpcRequest]

### Initialization Code

#### Example

```python
value = [
    JsonRpcRequest(
        method=Method.ENUM_TOOLSCALL,
        id=1,
        params=jsonpickle.decode('{"name":"get_product","arguments":{"shop":"vintageskates"}}')
    )
]
```

