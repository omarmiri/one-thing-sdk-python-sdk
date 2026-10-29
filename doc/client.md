
# Client Class Documentation

The following parameters are configurable for the API Client:

| Parameter | Type | Description |
|  --- | --- | --- |
| environment | [`Environment`](../README.md#environments) | The API environment. <br> **Default: `Environment.PRODUCTION`** |
| http_client_instance | `Union[Session, HttpClientProvider]` | The Http Client passed from the sdk user for making requests |
| override_http_client_configuration | `bool` | The value which determines to override properties of the passed Http Client from the sdk user |
| http_call_back | `HttpCallBack` | The callback value that is invoked before and after an HTTP call is made to an endpoint |
| timeout | `float` | The value to use for connection timeout. <br> **Default: 60** |
| max_retries | `int` | The number of times to retry an endpoint call if it fails. <br> **Default: 0** |
| backoff_factor | `float` | A backoff factor to apply between attempts after the second try. <br> **Default: 2** |
| retry_statuses | `Array of int` | The http statuses on which retry is to be done. <br> **Default: [408, 413, 429, 500, 502, 503, 504, 521, 522, 524, 408, 413, 429, 500, 502, 503, 504, 521, 522, 524]** |
| retry_methods | `Array of string` | The http methods on which retry is to be done. <br> **Default: ["GET", "PUT", "GET", "PUT"]** |
| proxy_settings | [`ProxySettings`](../doc/proxy-settings.md) | Optional proxy configuration to route HTTP requests through a proxy server. |
| admin_token_credentials | [`AdminTokenCredentials`](auth/custom-header-signature.md) | The credential object for Custom Header Signature |
| platform_key_credentials | [`PlatformKeyCredentials`](auth/oauth-2-bearer-token.md) | The credential object for OAuth 2 Bearer token |

The API client can be initialized as follows:

## Code-Based Client Initialization

```python
from onethingapi.configuration import Environment
from onethingapi.http.auth.admin_token import AdminTokenCredentials
from onethingapi.http.auth.platform_key import PlatformKeyCredentials
from onethingapi.onethingapi_client import OnethingapiClient

client = OnethingapiClient(
    admin_token_credentials=AdminTokenCredentials(
        x_admin_token='x-admin-token'
    ),
    platform_key_credentials=PlatformKeyCredentials(
        access_token='AccessToken'
    ),
    environment=Environment.PRODUCTION
)
```

## Environment-Based Client Initialization

```python
from onethingapi.onethingapi_client import OnethingapiClient

# Specify the path to your .env file if it’s located outside the project’s root directory.
client = OnethingapiClient.from_environment(dotenv_path='/path/to/.env')
```

See the [Environment-Based Client Initialization](../doc/environment-based-client-initialization.md) section for details.

## OneThing API Client

The gateway for the SDK. This class acts as a factory for the Apis and also holds the configuration of the SDK.

## Apis

| Name | Description |
|  --- | --- |
| accounts | Gets AccountsApi |
| shops | Gets ShopsApi |
| links | Gets LinksApi |
| products | Gets ProductsApi |
| checkout | Gets CheckoutApi |
| access_codes | Gets AccessCodesApi |
| orders | Gets OrdersApi |
| files | Gets FilesApi |
| agents | Gets AgentsApi |
| platforms | Gets PlatformsApi |

