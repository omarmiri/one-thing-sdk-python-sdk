
# Api Orders Capture 409 Error Exception

Not approved yet.

## Structure

`ApiOrdersCapture409ErrorException`

## Fields

| Name | Type | Tags | Description |
|  --- | --- | --- | --- |
| `status` | [`Status6`](../../doc/models/status-6.md) | Optional | `pending` until the buyer approves at PayPal. |

## Example

```python
try:
    # make the API call
except ApiOrdersCapture409ErrorException as e:
    print(e)
except ApiException as e:
    print(e)
```

