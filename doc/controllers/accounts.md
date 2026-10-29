# Accounts

Sign in as a seller with an email or a phone number. Shops made while signed in belong to the account.

```python
accounts_api = client.accounts
```

## Class Name

`AccountsApi`

## Methods

* [Sign In](../../doc/controllers/accounts.md#sign-in)
* [Sign Out](../../doc/controllers/accounts.md#sign-out)
* [Log In with Pay Pal](../../doc/controllers/accounts.md#log-in-with-pay-pal)


# Sign In

Signs in with an email address or a phone number, creating the account the first time. There's no password and no verification (sandbox). The response sets the `ot_session` cookie; shops created with it belong to the account and are listed on `/account`. Signing in with an email also claims older shops whose seller email matches. In a browser, sellers can instead use Log in with PayPal (`/api/account/paypal`), which also records the PayPal account their sales are paid into.

:information_source: **Note** This endpoint does not require authentication.

```python
def sign_in(self,
           body)
```

## Parameters

| Parameter | Type | Tags | Description |
|  --- | --- | --- | --- |
| `body` | [`ApiAccountSigninRequest`](../../doc/models/api-account-signin-request.md) | Body, Required | The email or phone number to sign in with. |

## Response Type

**200**: Signed in. The `ot_session` cookie is set.

[`ApiAccountSigninResponse`](../../doc/models/api-account-signin-response.md)

## Example Usage

```python
body = ApiAccountSigninRequest(
    identifier='maker@example.com'
)

result = accounts_api.sign_in(body)
print(result)
```

## Example Response *(as JSON)*

```json
{
  "id": "Vq3nN8cT0bLx2YwE",
  "email": "maker@example.com",
  "phone": null
}
```

## Errors

| HTTP Status Code | Error Description | Exception Class |
|  --- | --- | --- |
| 400 | Something in the request needs fixing; `error` says what. | [`ErrorResponseException`](../../doc/models/error-response-exception.md) |


# Sign Out

Ends this browser's session and clears the `ot_session` cookie.

:information_source: **Note** This endpoint does not require authentication.

```python
def sign_out(self)
```

## Response Type

**200**: Done.

[`Ok`](../../doc/models/ok.md)

## Example Usage

```python
result = accounts_api.sign_out()
print(result)
```

## Example Response *(as JSON)*

```json
{
  "ok": true
}
```


# Log In with Pay Pal

A link for a browser, not for code: redirects to PayPal's sign-in page. PayPal sends the seller back to `/api/account/paypal/callback`, which signs them in (creating the account the first time), records the PayPal account their sales are paid into, and redirects to `next`.

:information_source: **Note** This endpoint does not require authentication.

```python
def log_in_with_pay_pal(self,
                       next=None)
```

## Parameters

| Parameter | Type | Tags | Description |
|  --- | --- | --- | --- |
| `next` | `str` | Query, Optional | A path on this site to land on afterwards. Defaults to `/account`. |

## Response Type

**200**

`void`

## Example Usage

```python
next = '/account'

accounts_api.log_in_with_pay_pal(
    next=next
)
```

## Errors

| HTTP Status Code | Error Description | Exception Class |
|  --- | --- | --- |
| 503 | Log in with PayPal isn't switched on for this server. | [`ErrorResponseException`](../../doc/models/error-response-exception.md) |

