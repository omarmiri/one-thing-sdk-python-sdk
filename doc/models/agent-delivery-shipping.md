
# Agent Delivery Shipping

A physical product shipped to the buyer.

## Structure

`AgentDeliveryShipping`

## Fields

| Name | Type | Tags | Description |
|  --- | --- | --- | --- |
| `mtype` | `str` | Required, Constant | **Value**: `"shipping"` |
| `ship_to` | [`ShipTo`](../../doc/models/ship-to.md) | Optional | - |
| `fulfillment` | [`Fulfillment`](../../doc/models/fulfillment.md) | Required | - |
| `tracking` | [`Tracking`](../../doc/models/tracking.md) | Optional | - |

## Example

```python
from onethingapi.models.agent_delivery_shipping import AgentDeliveryShipping
from onethingapi.models.fulfillment import Fulfillment
from onethingapi.models.ship_to import ShipTo
from onethingapi.models.tracking import Tracking

agent_delivery_shipping = AgentDeliveryShipping(
    fulfillment=Fulfillment.TO_SHIP,
    ship_to=ShipTo(
        name='name6',
        address='address2'
    ),
    tracking=Tracking(
        carrier='carrier2',
        number='number8'
    )
)
```

