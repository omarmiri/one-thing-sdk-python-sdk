
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
    access_code='access_code2'
)
```

## AgentDeliveryDownload

### Initialization Code

#### Example

```python
value = AgentDeliveryDownload(
    download_url='download_url8'
)
```

## AgentDeliveryShipping

### Initialization Code

#### Example

```python
value = AgentDeliveryShipping(
    fulfillment=Fulfillment.TO_SHIP
)
```

