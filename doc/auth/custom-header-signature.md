
# Custom Header Signature



Documentation for accessing and setting credentials for AdminToken.

## Auth Credentials

| Name | Type | Description | Getter |
|  --- | --- | --- | --- |
| x-admin-token | `str` | The shop's admin token, returned once by `createShop`. Keep it secret. | `x_admin_token` |



**Note:** Auth credentials can be set using `AdminTokenCredentials` object, passed in as named parameter `admin_token_credentials` in the client initialization.

## Usage Example

### Client Initialization

You must provide credentials in the client as shown in the following code snippet.

```python
from onethingapi.http.auth.admin_token import AdminTokenCredentials
from onethingapi.onethingapi_client import OnethingapiClient

client = OnethingapiClient(
    admin_token_credentials=AdminTokenCredentials(
        x_admin_token='x-admin-token'
    )
)
```


