
# Api Account Signin Response

The signed-in account.

## Structure

`ApiAccountSigninResponse`

## Fields

| Name | Type | Tags | Description |
|  --- | --- | --- | --- |
| `id` | `str` | Required | The account's id. |
| `email` | `str` | Required | Lower-cased. |
| `phone` | `str` | Required | Digits, with a leading + if one was given. |

## Example

```python
from onethingapi.models.api_account_signin_response import ApiAccountSigninResponse

api_account_signin_response = ApiAccountSigninResponse(
    id='acc_Vq3nN8cT0bLx2YwE',
    email='maker@example.com',
    phone='+15555550123'
)
```

