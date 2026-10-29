
# Api Paypal Client Token Response

The client token.

## Structure

`ApiPaypalClientTokenResponse`

## Fields

| Name | Type | Tags | Description |
|  --- | --- | --- | --- |
| `client_token` | `str` | Required | Pass to `createInstance` in the PayPal JavaScript SDK v6. |

## Example

```python
from onethingapi.models.api_paypal_client_token_response import ApiPaypalClientTokenResponse

api_paypal_client_token_response = ApiPaypalClientTokenResponse(
    client_token='eyJraWQiOiJFWEFNUExFIn0.example.client-token'
)
```

