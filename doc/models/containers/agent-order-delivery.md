
# Agent Order Delivery

## Data Type

`AgentDeliveryAccessCode | AgentDeliveryDownload | AgentDeliveryShipping`

## Cases

| Type |
|  --- |
| [`AgentDeliveryAccessCode`](../../../doc/models/agent-delivery-access-code.md) |
| [`AgentDeliveryDownload`](../../../doc/models/agent-delivery-download.md) |
| [`AgentDeliveryShipping`](../../../doc/models/agent-delivery-shipping.md) |

## AgentDeliveryAccessCode

### Initialization Code

#### Example

```python
value = AgentDeliveryAccessCode(
    access_code='K7QF-M2XP-9HTD',
    start_url='https://www.miriogames.com/raptor-rush/?code=K7QF-M2XP-9HTD'
)
```

## AgentDeliveryDownload

### Initialization Code

#### Example

```python
value = AgentDeliveryDownload(
    download_url='https://one-thing-ash0.onrender.com/api/download/dl_4mQ8sT2vX9',
    note='Works 5 times over 14 days.'
)
```

## AgentDeliveryShipping

### Initialization Code

#### Example

```python
value = AgentDeliveryShipping(
    fulfillment=Fulfillment.TO_SHIP,
    ship_to=ShipTo(
        name='Sam Rivera',
        address='1 Main St, Springfield, IL, 62701, US'
    ),
    tracking=Tracking(
        carrier='USPS',
        number='9400111899223197428490'
    )
)
```

