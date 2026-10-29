# Checkout

Buyer-side PayPal checkout.

```python
checkout_api = client.checkout
```

## Class Name

`CheckoutApi`

## Methods

* [Get Pay Pal Client Token](../../doc/controllers/checkout.md#get-pay-pal-client-token)
* [Create Checkout Order](../../doc/controllers/checkout.md#create-checkout-order)
* [Capture Checkout Order](../../doc/controllers/checkout.md#capture-checkout-order)


# Get Pay Pal Client Token

A browser-safe client token for the PayPal JavaScript SDK v6
(`paypal.createInstance({ clientToken })`), bound to the requesting site's domain.
Shop pages call this before showing the PayPal button.

:information_source: **Note** This endpoint does not require authentication.

```python
def get_pay_pal_client_token(self)
```

## Response Type

**200**: A token for this site's domain.

[`ApiPaypalClientTokenResponse`](../../doc/models/api-paypal-client-token-response.md)

## Example Usage

```python
result = checkout_api.get_pay_pal_client_token()
print(result)
```

## Example Response *(as JSON)*

```json
{
  "clientToken": "eyJraWQiOiJFWEFNUExFIn0.example.client-token"
}
```

## Errors

| HTTP Status Code | Error Description | Exception Class |
|  --- | --- | --- |
| 502 | Gemini, PayPal or Channel3 failed or isn't configured. | [`ErrorException`](../../doc/models/error-exception.md) |
| 503 | Gemini, PayPal or Channel3 failed or isn't configured. | [`ErrorException`](../../doc/models/error-exception.md) |


# Create Checkout Order

Creates the PayPal order for one unit of a live shop's product. The amount always comes
from the shop, never from the caller. Pass the returned `id` to the PayPal JS SDK.

If the shop has buyer `options`, send one value for each. A sold-out combination answers 409.

:information_source: **Note** This endpoint does not require authentication.

```python
def create_checkout_order(self,
                         body)
```

## Parameters

| Parameter | Type | Tags | Description |
|  --- | --- | --- | --- |
| `body` | [`ApiOrdersRequest`](../../doc/models/api-orders-request.md) | Body, Required | - |

## Response Type

**200**: PayPal order created.

[`ApiOrdersResponse`](../../doc/models/api-orders-response.md)

## Example Usage

```python
body = ApiOrdersRequest(
    slug='raptorrush'
)

result = checkout_api.create_checkout_order(body)
print(result)
```

## Example Response *(as JSON)*

```json
{
  "id": "5O190127TN364715T"
}
```

## Errors

| HTTP Status Code | Error Description | Exception Class |
|  --- | --- | --- |
| 400 | Something in the request needs fixing; `error` says what. | [`ErrorException`](../../doc/models/error-exception.md) |
| 404 | No such shop, or the admin token or API key doesn't match it. | [`ErrorException`](../../doc/models/error-exception.md) |
| 409 | Taken or unavailable (a link name, or a sold-out product). | [`ErrorException`](../../doc/models/error-exception.md) |
| 429 | Over this network's cap for the call (see **Limits**). Retry after `Retry-After` seconds. | [`ErrorException`](../../doc/models/error-exception.md) |
| 502 | Gemini, PayPal or Channel3 failed or isn't configured. | [`ErrorException`](../../doc/models/error-exception.md) |
| 503 | Gemini, PayPal or Channel3 failed or isn't configured. | [`ErrorException`](../../doc/models/error-exception.md) |


# Capture Checkout Order

Call after the buyer approves. Records the sale; digital orders get a download link or access code.
Safe to call repeatedly: before approval it answers 409, so a page can poll it while the PayPal window is open.

:information_source: **Note** This endpoint does not require authentication.

```python
def capture_checkout_order(self,
                          paypal_order_id)
```

## Parameters

| Parameter | Type | Tags | Description |
|  --- | --- | --- | --- |
| `paypal_order_id` | `str` | Template, Required | The PayPal order id that `createCheckoutOrder` returned. |

## Response Type

**200**: Paid.

[`ApiOrdersCaptureResponse`](../../doc/models/api-orders-capture-response.md)

## Example Usage

```python
paypal_order_id = '5O190127TN364715T'

result = checkout_api.capture_checkout_order(paypal_order_id)
print(result)
```

## Example Response *(as JSON)*

```json
{
  "orderId": "pX4kR9tVb2nQ7sLe",
  "status": "paid"
}
```

## Errors

| HTTP Status Code | Error Description | Exception Class |
|  --- | --- | --- |
| 402 | Something in the request needs fixing; `error` says what. | [`ErrorException`](../../doc/models/error-exception.md) |
| 404 | No such shop, or the admin token or API key doesn't match it. | [`ErrorException`](../../doc/models/error-exception.md) |
| 409 | The buyer hasn't approved the order yet. | [`ApiOrdersCapture409ErrorException`](../../doc/models/api-orders-capture-409-error-exception.md) |
| 410 | The last unit (or the last of the buyer's combination) sold while they were paying, or the PayPal checkout expired before they paid. The payment isn't captured, so the buyer isn't charged. | [`ErrorException`](../../doc/models/error-exception.md) |
| 422 | The buyer's funding source was declined (`INSTRUMENT_DECLINED`); they can try another. | [`ErrorException`](../../doc/models/error-exception.md) |
| 502 | Gemini, PayPal or Channel3 failed or isn't configured. | [`ErrorException`](../../doc/models/error-exception.md) |

