# Orders

The seller's orders, fulfilment and PayPal webhook log.

```python
orders_api = client.orders
```

## Class Name

`OrdersApi`

## Methods

* [List Orders](../../doc/controllers/orders.md#list-orders)
* [Mark Order Shipped](../../doc/controllers/orders.md#mark-order-shipped)
* [Refund Order](../../doc/controllers/orders.md#refund-order)
* [List Webhook Events](../../doc/controllers/orders.md#list-webhook-events)


# List Orders

Newest first. Checkouts that were never approved are left out.

```python
def list_orders(self,
               slug)
```

## Authentication

This endpoint requires [AdminToken](../../doc/auth/custom-header-signature.md) **OR** [PlatformKey](../../doc/auth/oauth-2-bearer-token.md)

## Parameters

| Parameter | Type | Tags | Description |
|  --- | --- | --- | --- |
| `slug` | `str` | Template, Required | The shop's link name (current or former). |

## Response Type

**200**: Orders.

[`List[Order]`](../../doc/models/order.md)

## Example Usage

```python
slug = 'raptorrush'

result = orders_api.list_orders(slug)
print(result)
```

## Example Response *(as JSON)*

```json
[
  {
    "id": "pX4kR9tVb2nQ7sLe",
    "paypal_order_id": "5O190127TN364715T",
    "status": "paid",
    "amount_cents": 25500,
    "shipping_cents": 1500,
    "currency": "USD",
    "buyer_email": "buyer@example.com",
    "buyer_name": "Sam Rivera",
    "shipping_address": {
      "address_line_1": "1 Main St",
      "admin_area_2": "Springfield",
      "admin_area_1": "IL",
      "postal_code": "62701",
      "country_code": "US"
    },
    "capture_id": "3C679366HH908993F",
    "fulfillment_status": "to_ship",
    "carrier": null,
    "tracking_number": null,
    "tracking_synced": false,
    "downloads": 0,
    "access_code": null,
    "code_uses": 0,
    "channel": "agent",
    "options": {
      "Size": "8"
    },
    "paid_at": "2026-10-22T02:41:37Z",
    "created_at": "2026-10-22T02:38:05Z"
  }
]
```

## Errors

| HTTP Status Code | Error Description | Exception Class |
|  --- | --- | --- |
| 404 | No such shop, or the admin token or API key doesn't match it. | [`ErrorException`](../../doc/models/error-exception.md) |


# Mark Order Shipped

Saves the tracking number and pushes it to PayPal, so the buyer sees it in PayPal.

```python
def mark_order_shipped(self,
                      slug,
                      order_id,
                      body)
```

## Authentication

This endpoint requires [AdminToken](../../doc/auth/custom-header-signature.md) **OR** [PlatformKey](../../doc/auth/oauth-2-bearer-token.md)

## Parameters

| Parameter | Type | Tags | Description |
|  --- | --- | --- | --- |
| `slug` | `str` | Template, Required | The shop's link name (current or former). |
| `order_id` | `str` | Template, Required | OneThing's order id (`Order.id`). |
| `body` | [`ApiShopsOrdersShipRequest`](../../doc/models/api-shops-orders-ship-request.md) | Body, Required | - |

## Response Type

**200**: Shipped.

[`ApiShopsOrdersShipResponse`](../../doc/models/api-shops-orders-ship-response.md)

## Example Usage

```python
slug = 'raptorrush'

order_id = 'pX4kR9tVb2nQ7sLe'

body = ApiShopsOrdersShipRequest(
    carrier=Carrier.USPS,
    tracking_number='9400111899223817362315'
)

result = orders_api.mark_order_shipped(
    slug,
    order_id,
    body
)
print(result)
```

## Example Response *(as JSON)*

```json
{
  "ok": true,
  "synced": true
}
```

## Errors

| HTTP Status Code | Error Description | Exception Class |
|  --- | --- | --- |
| 400 | Something in the request needs fixing; `error` says what. | [`ErrorException`](../../doc/models/error-exception.md) |
| 404 | No such shop, or the admin token or API key doesn't match it. | [`ErrorException`](../../doc/models/error-exception.md) |


# Refund Order

Refunds the whole payment through PayPal and marks the order `refunded`. When PayPal only lets the paid account refund it (the money went to a PayPal email the seller typed in, not a connected account), the reply is a 409 with `refundInPayPal: true`. Refund it in your PayPal account, then call this again with `{"record": true}`, which only marks it refunded here. Sends the `order.refunded` event to the shop's Zapier hook.

```python
def refund_order(self,
                slug,
                order_id,
                body=None)
```

## Authentication

This endpoint requires [AdminToken](../../doc/auth/custom-header-signature.md) **OR** [PlatformKey](../../doc/auth/oauth-2-bearer-token.md)

## Parameters

| Parameter | Type | Tags | Description |
|  --- | --- | --- | --- |
| `slug` | `str` | Template, Required | The shop's link name (current or former). |
| `order_id` | `str` | Template, Required | OneThing's order id (`Order.id`). |
| `body` | [`ApiShopsOrdersRefundRequest`](../../doc/models/api-shops-orders-refund-request.md) | Body, Optional | - |

## Response Type

**200**: Refunded.

[`ApiShopsOrdersRefundResponse`](../../doc/models/api-shops-orders-refund-response.md)

## Example Usage

```python
slug = 'raptorrush'

order_id = 'pX4kR9tVb2nQ7sLe'

body = ApiShopsOrdersRefundRequest()

result = orders_api.refund_order(
    slug,
    order_id,
    body=body
)
print(result)
```

## Example Response *(as JSON)*

```json
{
  "ok": true,
  "refundId": "1JU08902781691411"
}
```

## Errors

| HTTP Status Code | Error Description | Exception Class |
|  --- | --- | --- |
| 404 | No such shop or order, or the token doesn't match the shop. | [`ErrorException`](../../doc/models/error-exception.md) |
| 409 | Not refundable here; `error` says why. | [`ApiShopsOrdersRefund409ErrorException`](../../doc/models/api-shops-orders-refund-409-error-exception.md) |


# List Webhook Events

The last 50 PayPal webhook deliveries about this shop's orders, with signature results.

```python
def list_webhook_events(self,
                       slug)
```

## Authentication

This endpoint requires [AdminToken](../../doc/auth/custom-header-signature.md) **OR** [PlatformKey](../../doc/auth/oauth-2-bearer-token.md)

## Parameters

| Parameter | Type | Tags | Description |
|  --- | --- | --- | --- |
| `slug` | `str` | Template, Required | The shop's link name (current or former). |

## Response Type

**200**: Events, newest first.

[`List[WebhookEvent]`](../../doc/models/webhook-event.md)

## Example Usage

```python
slug = 'raptorrush'

result = orders_api.list_webhook_events(slug)
print(result)
```

## Example Response *(as JSON)*

```json
[
  {
    "id": "WH-2WR32451HC0233532-67976317FL4543714",
    "event_type": "PAYMENT.CAPTURE.COMPLETED",
    "paypal_order_id": "5O190127TN364715T",
    "summary": "255.00 USD",
    "verified": true,
    "outcome": "Confirmed: order already paid",
    "received_at": "2026-10-22T02:41:40Z"
  }
]
```

## Errors

| HTTP Status Code | Error Description | Exception Class |
|  --- | --- | --- |
| 404 | No such shop, or the admin token or API key doesn't match it. | [`ErrorException`](../../doc/models/error-exception.md) |

