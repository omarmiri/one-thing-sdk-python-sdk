
# Status 2

`declined`: PayPal declined it, nothing charged, the buyer can open `pay_url` again. `sold_out`: it sold out before the payment was captured. `expired`: the PayPal checkout expired; create a new order. `failed`: PayPal couldn't be reached; ask again.

## Enumeration

`Status2`

## Fields

| Name |
|  --- |
| `AWAITING_BUYER_APPROVAL` |
| `PAID` |
| `DECLINED` |
| `SOLD_OUT` |
| `EXPIRED` |
| `FAILED` |

## Example

```python
from onethingapi.models.status_2 import Status2

status_2 = Status2.EXPIRED
```

