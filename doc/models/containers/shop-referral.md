
# Shop Referral

## Data Type

`Referral`

## Cases

| Type |
|  --- |
| [`Referral`](../../../doc/models/referral.md) |

## Referral

### Initialization Code

#### Example

```python
value = Referral(
    product_id='ch3_7f2a9c1e',
    title='Trail Running Vest 5L',
    offers=[
        Offer(
            domain='rei.com',
            url='https://buy.trychannel3.com/r/abc123',
            price=240,
            currency='USD',
            in_stock=True,
            commission=0.08
        )
    ],
    brand='Salomon',
    image='https://images.example.com/vest.jpg'
)
```

