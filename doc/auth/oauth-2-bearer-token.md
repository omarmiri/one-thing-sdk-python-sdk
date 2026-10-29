
# OAuth 2 Bearer token



Documentation for accessing and setting credentials for PlatformKey.

## Auth Credentials

| Name | Type | Description | Getter |
|  --- | --- | --- | --- |
| AccessToken | `str` | The OAuth 2.0 Access Token to use for API requests. | `access_token` |



**Note:** Auth credentials can be set using `PlatformKeyCredentials` object, passed in as named parameter `platform_key_credentials` in the client initialization.

## Usage Example

### Client Initialization

You must provide credentials in the client as shown in the following code snippet.

```python
from onethingapi.http.auth.platform_key import PlatformKeyCredentials
from onethingapi.onethingapi_client import OnethingapiClient

client = OnethingapiClient(
    platform_key_credentials=PlatformKeyCredentials(
        access_token='AccessToken'
    )
)
```


