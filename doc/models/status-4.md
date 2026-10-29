
# Status 4

`created` until paid; `failed` if PayPal declined; `refunded` after a refund.

## Enumeration

`Status4`

## Fields

| Name |
|  --- |
| `CREATED` |
| `PAID` |
| `FAILED` |
| `REFUNDED` |

## Example

```python
from onethingapi.models.status_4 import Status4

status_4 = Status4.FAILED
```

