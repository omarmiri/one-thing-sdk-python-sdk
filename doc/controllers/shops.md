# Shops

Create a shop and manage it as its seller.

```python
shops_api = client.shops
```

## Class Name

`ShopsApi`

## Methods

* [Create Shop](../../doc/controllers/shops.md#create-shop)
* [Get Shop](../../doc/controllers/shops.md#get-shop)
* [Update Shop](../../doc/controllers/shops.md#update-shop)
* [Refine Shop Design](../../doc/controllers/shops.md#refine-shop-design)
* [Regenerate Hero Art](../../doc/controllers/shops.md#regenerate-hero-art)
* [Upload Digital File](../../doc/controllers/shops.md#upload-digital-file)
* [Add Photos](../../doc/controllers/shops.md#add-photos)
* [Set Photo Order](../../doc/controllers/shops.md#set-photo-order)
* [Check Missing Details](../../doc/controllers/shops.md#check-missing-details)
* [Match Color Photos](../../doc/controllers/shops.md#match-color-photos)
* [Set Color Photos](../../doc/controllers/shops.md#set-color-photos)
* [Connect Pay Pal](../../doc/controllers/shops.md#connect-pay-pal)
* [Get Pay Pal Connection](../../doc/controllers/shops.md#get-pay-pal-connection)
* [Disconnect Pay Pal](../../doc/controllers/shops.md#disconnect-pay-pal)


# Create Shop

Starts a draft shop from one of three sources. Gemini designs the page and guesses the
setup; check it with `getShop`, adjust with `updateShop`, then go live.

Sent with a session cookie from `signIn`, the shop belongs to that account, which also
becomes its seller email (and PayPal email, after Log in with PayPal) unless you give one.

- `source=photo`: a `photo` and/or a `description` of your own product.
- `source=link`: a `url`. If Channel3 recognises it as a store's product page, the shop
  becomes a recommendation (`product_type: referral`); otherwise the page is read and you
  sell the product yourself with PayPal.
- `source=channel3`: a `productId` from `searchProducts` (a recommendation).

Takes 15–40 seconds. Hero art, if available, is generated afterwards (`hero_status`).

**Platforms:** sent with a platform API key, the shop belongs to the key's account, so the
key can manage it from then on (no need to keep the admin token). It's made for one of the
platform's sellers, so it inherits nothing from the account: set `paypal_email` or call
`connectPayPal` for that seller.

```python
def create_shop(self,
               source,
               photo=None,
               description=None,
               url=None,
               product_id=None,
               slug=None,
               mtype="auto",
               delivery=None,
               access_url=None,
               price=None,
               shipping=None,
               stock=None,
               ship_countries=None,
               paypal_email=None,
               seller_email=None,
               digital_file=None)
```

## Authentication

This endpoint requires [PlatformKey](../../doc/auth/oauth-2-bearer-token.md)

## Parameters

| Parameter | Type | Tags | Description |
|  --- | --- | --- | --- |
| `source` | [`Source`](../../doc/models/source.md) | Form, Required | What the shop starts from: a photo (with an optional description), a product link, or a Channel3 product to recommend. |
| `photo` | `typing.BinaryIO` | Form, Optional | `source=photo`: the product photo, up to 8 MB. |
| `description` | `str` | Form, Optional | `source=photo`: a sentence or two about the product. Required if there is no photo. |
| `url` | `str` | Form, Optional | `source=link`: a product page, or your own app or game page. |
| `product_id` | `str` | Form, Optional | `source=channel3`: a product id from `searchProducts`. |
| `slug` | `str` | Form, Optional | The link name you want. If omitted, the AI suggests one. |
| `mtype` | [`Type`](../../doc/models/type.md) | Form, Optional | `physical` ships, `digital` is a file or an access code, `auto` lets the AI decide.<br><br>**Default**: `"auto"` |
| `delivery` | [`Delivery`](../../doc/models/delivery.md) | Form, Optional | For digital products. If omitted, the AI guesses. |
| `access_url` | `str` | Form, Optional | Where buyers use an access code. |
| `price` | `float` | Form, Optional | USD. If omitted, the AI suggests a price. |
| `shipping` | `float` | Form, Optional | Physical products: shipping per order, in USD. If omitted, the AI suggests it. |
| `stock` | `int` | Form, Optional | How many are for sale. Leave out for unlimited. |
| `ship_countries` | `str` | Form, Optional | Physical products: comma-separated ISO country codes to ship to. Empty means anywhere PayPal ships. |
| `paypal_email` | `str` | Form, Optional | The PayPal account that gets paid, if the seller doesn't connect one with `connectPayPal`. |
| `seller_email` | `str` | Form, Optional | Where order notifications go. |
| `digital_file` | `typing.BinaryIO` | Form, Optional | Digital products sold as a file: the file buyers download, up to 25 MB. Can also be added later with `uploadDigitalFile`. |

## Response Type

**200**: Draft created.

[`CreatedShop`](../../doc/models/created-shop.md)

## Example Usage

```python
source = Source.PHOTO

mtype = Type.PHYSICAL

ship_countries = 'US'

result = shops_api.create_shop(
    source,
    mtype=mtype,
    ship_countries=ship_countries
)
print(result)
```

## Example Response *(as JSON)*

```json
{
  "slug": "vintageskates",
  "token": "3fJ9xQm2LwP8vR1tZk7cN4bY6dHs0aEu",
  "manageUrl": "/manage/vintageskates?token=3fJ9xQm2LwP8vR1tZk7cN4bY6dHs0aEu"
}
```

## Errors

| HTTP Status Code | Error Description | Exception Class |
|  --- | --- | --- |
| 400 | Something in the request needs fixing; `error` says what. | [`ErrorResponseException`](../../doc/models/error-response-exception.md) |
| 409 | Taken or unavailable (a link name, or a sold-out product). | [`ErrorResponseException`](../../doc/models/error-response-exception.md) |
| 429 | Over this network's cap for the call (see **Limits**). Retry after `Retry-After` seconds. | [`ErrorResponseException`](../../doc/models/error-response-exception.md) |
| 502 | Gemini, PayPal or Channel3 failed or isn't configured. | [`ErrorResponseException`](../../doc/models/error-response-exception.md) |


# Get Shop

Everything about the shop, including the AI's design spec and guesses.

```python
def get_shop(self,
            slug)
```

## Authentication

This endpoint requires [AdminToken](../../doc/auth/custom-header-signature.md) **OR** [PlatformKey](../../doc/auth/oauth-2-bearer-token.md)

## Parameters

| Parameter | Type | Tags | Description |
|  --- | --- | --- | --- |
| `slug` | `str` | Template, Required | The shop's link name (current or former). |

## Response Type

**200**: The shop.

[`Shop`](../../doc/models/shop.md)

## Example Usage

```python
slug = 'vintageskates'

result = shops_api.get_shop(slug)
print(result)
```

## Example Response *(as JSON)*

```json
{
  "id": "Hn2c8QvL0xTzR4pW",
  "slug": "vintageskates",
  "status": "live",
  "product_type": "physical",
  "price_cents": 24000,
  "currency": "USD",
  "shipping_cents": 1500,
  "ship_countries": "US",
  "stock": null,
  "delivery": "file",
  "access_url": null,
  "paypal_email": "seller@example.com",
  "seller_email": "seller@example.com",
  "paypal_merchant_id": "7MZJ4QXN8K2LA",
  "paypal_status": {
    "receivable": true,
    "emailConfirmed": true,
    "checkedAt": "2026-10-21T18:04:11Z"
  },
  "zapier_hook_url": null,
  "in_gallery": true,
  "account_id": "Vq3nN8cT0bLx2YwE",
  "options": [
    {
      "name": "Size",
      "kind": "size",
      "values": [
        {
          "label": "7"
        },
        {
          "label": "8"
        },
        {
          "label": "9"
        }
      ]
    }
  ],
  "option_stock": {
    "7": 3,
    "8": 0,
    "9": 6
  },
  "suggestions": null,
  "photo_blob": "LFRvGuTU3D8i334X",
  "gallery_blobs": [
    "zrySajNyao6_j11x",
    "SuqcgNv64HWN8H6e"
  ],
  "hero_blob": null,
  "hero_status": "none",
  "hero_error": null,
  "ai_source": "gemini",
  "source_url": null,
  "referral": null,
  "spec": {
    "productType": "physical",
    "productName": "Vintage Cream and Red Roller Skates",
    "layout": "editorial",
    "palette": {
      "background": "#f6efe4",
      "surface": "#fffaf2",
      "text": "#2b1d14",
      "muted": "#7a6455",
      "accent": "#b3261e",
      "accentText": "#ffffff"
    },
    "fonts": {
      "heading": "Playfair Display",
      "body": "Inter"
    },
    "eyebrow": "One pair, restored",
    "headline": "Classic quad skates crafted with walnut burl heels",
    "subheadline": "A vintage pair of skates featuring cream leather, bold red trim, and durable quad wheels.",
    "story": "Each pair combines soft cream leather with distinct red accents and a sculpted walnut burl heel base.",
    "bullets": [
      "Handmade cream leather upper with rich red trim",
      "Sculpted walnut burl heel structure for stability"
    ],
    "details": [
      {
        "label": "Materials",
        "value": "Leather upper, walnut burl heel, rubber wheels"
      }
    ],
    "faq": [
      {
        "q": "Are these suitable for outdoor skating?",
        "a": "Yes, on indoor rink floors and paved outdoor paths."
      }
    ],
    "ctaLabel": "Buy the skates",
    "suggestedPriceUsd": 240,
    "suggestedShippingUsd": 15,
    "imageAlt": "Cream leather quad roller skates with red trim"
  },
  "created_at": "2026-10-19T15:22:08Z"
}
```

## Errors

| HTTP Status Code | Error Description | Exception Class |
|  --- | --- | --- |
| 404 | No such shop, or the admin token or API key doesn't match it. | [`ErrorResponseException`](../../doc/models/error-response-exception.md) |


# Update Shop

Changes only the fields you send. Renaming `slug` keeps the old link working (it
redirects). Set `status: live` to publish; a digital product needs its file (or, for
access codes, `access_url`) first.

```python
def update_shop(self,
               slug,
               body)
```

## Authentication

This endpoint requires [AdminToken](../../doc/auth/custom-header-signature.md) **OR** [PlatformKey](../../doc/auth/oauth-2-bearer-token.md)

## Parameters

| Parameter | Type | Tags | Description |
|  --- | --- | --- | --- |
| `slug` | `str` | Template, Required | The shop's link name (current or former). |
| `body` | [`ShopUpdate`](../../doc/models/shop-update.md) | Body, Required | The fields to change; anything left out stays as it is. |

## Response Type

**200**: Saved.

[`ApiShopsResponse`](../../doc/models/api-shops-response.md)

## Example Usage

```python
slug = 'vintageskates'

body = ShopUpdate(
    status=Status.LIVE
)

result = shops_api.update_shop(
    slug,
    body
)
print(result)
```

## Example Response *(as JSON)*

```json
{
  "ok": true,
  "slug": "vintageskates"
}
```

## Errors

| HTTP Status Code | Error Description | Exception Class |
|  --- | --- | --- |
| 400 | Something in the request needs fixing; `error` says what. | [`ErrorResponseException`](../../doc/models/error-response-exception.md) |
| 404 | No such shop, or the admin token or API key doesn't match it. | [`ErrorResponseException`](../../doc/models/error-response-exception.md) |


# Refine Shop Design

"Make it warmer", "shorter copy", "more premium". Gemini edits the design spec.

```python
def refine_shop_design(self,
                      slug,
                      body)
```

## Authentication

This endpoint requires [AdminToken](../../doc/auth/custom-header-signature.md) **OR** [PlatformKey](../../doc/auth/oauth-2-bearer-token.md)

## Parameters

| Parameter | Type | Tags | Description |
|  --- | --- | --- | --- |
| `slug` | `str` | Template, Required | The shop's link name (current or former). |
| `body` | [`ApiShopsRefineRequest`](../../doc/models/api-shops-refine-request.md) | Body, Required | The design change, in words. |

## Response Type

**200**: The new design.

[`ApiShopsRefineResponse`](../../doc/models/api-shops-refine-response.md)

## Example Usage

```python
slug = 'vintageskates'

body = ApiShopsRefineRequest(
    instruction='Make it feel more premium'
)

result = shops_api.refine_shop_design(
    slug,
    body
)
print(result)
```

## Example Response *(as JSON)*

```json
{
  "spec": {
    "productType": "physical",
    "productName": "Vintage Cream and Red Roller Skates",
    "layout": "editorial",
    "palette": {
      "background": "#f6efe4",
      "surface": "#fffaf2",
      "text": "#2b1d14",
      "muted": "#7a6455",
      "accent": "#b3261e",
      "accentText": "#ffffff"
    },
    "fonts": {
      "heading": "Playfair Display",
      "body": "Inter"
    },
    "eyebrow": "One pair, restored",
    "headline": "Classic quad skates crafted with walnut burl heels",
    "subheadline": "A vintage pair of skates featuring cream leather, bold red trim, and durable quad wheels.",
    "story": "Each pair combines soft cream leather with distinct red accents and a sculpted walnut burl heel base.",
    "bullets": [
      "Handmade cream leather upper with rich red trim",
      "Sculpted walnut burl heel structure for stability"
    ],
    "details": [
      {
        "label": "Materials",
        "value": "Leather upper, walnut burl heel, rubber wheels"
      }
    ],
    "faq": [
      {
        "q": "Are these suitable for outdoor skating?",
        "a": "Yes, on indoor rink floors and paved outdoor paths."
      }
    ],
    "ctaLabel": "Buy the skates",
    "suggestedPriceUsd": 240,
    "suggestedShippingUsd": 15,
    "imageAlt": "Cream leather quad roller skates with red trim"
  }
}
```

## Errors

| HTTP Status Code | Error Description | Exception Class |
|  --- | --- | --- |
| 400 | Something in the request needs fixing; `error` says what. | [`ErrorResponseException`](../../doc/models/error-response-exception.md) |
| 404 | No such shop, or the admin token or API key doesn't match it. | [`ErrorResponseException`](../../doc/models/error-response-exception.md) |
| 429 | Over this network's cap for the call (see **Limits**). Retry after `Retry-After` seconds. | [`ErrorResponseException`](../../doc/models/error-response-exception.md) |
| 502 | Gemini, PayPal or Channel3 failed or isn't configured. | [`ErrorResponseException`](../../doc/models/error-response-exception.md) |


# Regenerate Hero Art

Starts generation in the background. Poll `getShop` for `hero_status`.

```python
def regenerate_hero_art(self,
                       slug)
```

## Authentication

This endpoint requires [AdminToken](../../doc/auth/custom-header-signature.md) **OR** [PlatformKey](../../doc/auth/oauth-2-bearer-token.md)

## Parameters

| Parameter | Type | Tags | Description |
|  --- | --- | --- | --- |
| `slug` | `str` | Template, Required | The shop's link name (current or former). |

## Response Type

**200**: Done.

[`Ok`](../../doc/models/ok.md)

## Example Usage

```python
slug = 'vintageskates'

result = shops_api.regenerate_hero_art(slug)
print(result)
```

## Example Response *(as JSON)*

```json
{
  "ok": true
}
```

## Errors

| HTTP Status Code | Error Description | Exception Class |
|  --- | --- | --- |
| 400 | Something in the request needs fixing; `error` says what. | [`ErrorResponseException`](../../doc/models/error-response-exception.md) |
| 404 | No such shop, or the admin token or API key doesn't match it. | [`ErrorResponseException`](../../doc/models/error-response-exception.md) |
| 429 | Over this network's cap for the call (see **Limits**). Retry after `Retry-After` seconds. | [`ErrorResponseException`](../../doc/models/error-response-exception.md) |


# Upload Digital File

Uploads or replaces a digital product's file, up to 25 MB. Each paid order gets a download link for it.

```python
def upload_digital_file(self,
                       slug,
                       file)
```

## Authentication

This endpoint requires [AdminToken](../../doc/auth/custom-header-signature.md) **OR** [PlatformKey](../../doc/auth/oauth-2-bearer-token.md)

## Parameters

| Parameter | Type | Tags | Description |
|  --- | --- | --- | --- |
| `slug` | `str` | Template, Required | The shop's link name (current or former). |
| `file` | `typing.BinaryIO` | Form, Required | Up to 25 MB. |

## Response Type

**200**: Uploaded.

[`ApiShopsFileResponse`](../../doc/models/api-shops-file-response.md)

## Example Usage

```python
slug = 'vintageskates'

file = FileWrapper(Path('dummy_file').open('rb'), 'optional-content-type')

result = shops_api.upload_digital_file(
    slug,
    file
)
print(result)
```

## Example Response *(as JSON)*

```json
{
  "ok": true,
  "filename": "raptor-rush-soundtrack.zip"
}
```

## Errors

| HTTP Status Code | Error Description | Exception Class |
|  --- | --- | --- |
| 400 | Something in the request needs fixing; `error` says what. | [`ErrorResponseException`](../../doc/models/error-response-exception.md) |
| 404 | No such shop, or the admin token or API key doesn't match it. | [`ErrorResponseException`](../../doc/models/error-response-exception.md) |


# Add Photos

Adds one or more photos after the cover. Each is turned upright, resized to at most 2000 px and stored as WebP. A shop holds up to 8 photos; buyers swipe through them on the shop page. Not for recommendations, which show the retailer's photos.

```python
def add_photos(self,
              slug,
              photo)
```

## Authentication

This endpoint requires [AdminToken](../../doc/auth/custom-header-signature.md) **OR** [PlatformKey](../../doc/auth/oauth-2-bearer-token.md)

## Parameters

| Parameter | Type | Tags | Description |
|  --- | --- | --- | --- |
| `slug` | `str` | Template, Required | The shop's link name (current or former). |
| `photo` | `typing.BinaryIO` | Form, Required | An image, up to 15 MB. The endpoint also accepts the field repeated, to add several in one request. |

## Response Type

**200**: The shop's photos, cover first.

[`ShopPhotos`](../../doc/models/shop-photos.md)

## Example Usage

```python
slug = 'vintageskates'

photo = FileWrapper(Path('dummy_file').open('rb'), 'optional-content-type')

result = shops_api.add_photos(
    slug,
    photo
)
print(result)
```

## Example Response *(as JSON)*

```json
{
  "photos": [
    {
      "id": "LFRvGuTU3D8i334X",
      "url": "/api/blobs/LFRvGuTU3D8i334X"
    },
    {
      "id": "zrySajNyao6_j11x",
      "url": "/api/blobs/zrySajNyao6_j11x"
    }
  ]
}
```

## Errors

| HTTP Status Code | Error Description | Exception Class |
|  --- | --- | --- |
| 400 | Something in the request needs fixing; `error` says what. | [`ErrorResponseException`](../../doc/models/error-response-exception.md) |
| 404 | No such shop, or the admin token or API key doesn't match it. | [`ErrorResponseException`](../../doc/models/error-response-exception.md) |


# Set Photo Order

Sets the photo order; the first becomes the cover. Leaving a photo out removes it.

```python
def set_photo_order(self,
                   slug,
                   body)
```

## Authentication

This endpoint requires [AdminToken](../../doc/auth/custom-header-signature.md) **OR** [PlatformKey](../../doc/auth/oauth-2-bearer-token.md)

## Parameters

| Parameter | Type | Tags | Description |
|  --- | --- | --- | --- |
| `slug` | `str` | Template, Required | The shop's link name (current or former). |
| `body` | [`ApiShopsPhotosRequest`](../../doc/models/api-shops-photos-request.md) | Body, Required | Every photo id, in the new order. |

## Response Type

**200**: The shop's photos, cover first.

[`ShopPhotos`](../../doc/models/shop-photos.md)

## Example Usage

```python
slug = 'vintageskates'

body = ApiShopsPhotosRequest(
    photos=[
        'zrySajNyao6_j11x',
        'LFRvGuTU3D8i334X',
        'SuqcgNv64HWN8H6e'
    ]
)

result = shops_api.set_photo_order(
    slug,
    body
)
print(result)
```

## Example Response *(as JSON)*

```json
{
  "photos": [
    {
      "id": "LFRvGuTU3D8i334X",
      "url": "/api/blobs/LFRvGuTU3D8i334X"
    },
    {
      "id": "zrySajNyao6_j11x",
      "url": "/api/blobs/zrySajNyao6_j11x"
    }
  ]
}
```

## Errors

| HTTP Status Code | Error Description | Exception Class |
|  --- | --- | --- |
| 400 | Something in the request needs fixing; `error` says what. | [`ErrorResponseException`](../../doc/models/error-response-exception.md) |
| 404 | No such shop, or the admin token or API key doesn't match it. | [`ErrorResponseException`](../../doc/models/error-response-exception.md) |


# Check Missing Details

Asks Gemini what buyers will want to choose (sizes, colours) and what they'll ask that the
listing doesn't say (dimensions, materials). `createShop` already does this once; call it
again after editing the product. The result is saved as the shop's `suggestions`.

Nothing changes on the shop page until the seller confirms: save options with `updateShop`
(`options`), and answer the questions with `updateShop` (`facts`). Not for recommendations.

```python
def check_missing_details(self,
                         slug)
```

## Authentication

This endpoint requires [AdminToken](../../doc/auth/custom-header-signature.md) **OR** [PlatformKey](../../doc/auth/oauth-2-bearer-token.md)

## Parameters

| Parameter | Type | Tags | Description |
|  --- | --- | --- | --- |
| `slug` | `str` | Template, Required | The shop's link name (current or former). |

## Response Type

**200**: The suggestions.

[`Suggestions`](../../doc/models/suggestions.md)

## Example Usage

```python
slug = 'vintageskates'

result = shops_api.check_missing_details(slug)
print(result)
```

## Example Response *(as JSON)*

```json
{
  "oneOfAKind": false,
  "options": [
    {
      "name": "Size",
      "kind": "size",
      "values": [
        {
          "label": "7"
        },
        {
          "label": "8"
        },
        {
          "label": "9"
        }
      ],
      "fromSeller": false
    }
  ],
  "missingFacts": [
    {
      "label": "Wheel size",
      "question": "How big are the wheels?",
      "placeholder": "57 mm"
    }
  ]
}
```

## Errors

| HTTP Status Code | Error Description | Exception Class |
|  --- | --- | --- |
| 400 | Something in the request needs fixing; `error` says what. | [`ErrorResponseException`](../../doc/models/error-response-exception.md) |
| 404 | No such shop, or the admin token or API key doesn't match it. | [`ErrorResponseException`](../../doc/models/error-response-exception.md) |
| 429 | Over this network's cap for the call (see **Limits**). Retry after `Retry-After` seconds. | [`ErrorResponseException`](../../doc/models/error-response-exception.md) |
| 502 | Gemini, PayPal or Channel3 failed or isn't configured. | [`ErrorResponseException`](../../doc/models/error-response-exception.md) |


# Match Color Photos

Gemini looks at the shop's photos and says which one shows each colour, so buyers who pick a colour see it. Suggests only; save the matches with `setColorPhotos`. Needs at least two photos.

```python
def match_color_photos(self,
                      slug,
                      body)
```

## Authentication

This endpoint requires [AdminToken](../../doc/auth/custom-header-signature.md) **OR** [PlatformKey](../../doc/auth/oauth-2-bearer-token.md)

## Parameters

| Parameter | Type | Tags | Description |
|  --- | --- | --- | --- |
| `slug` | `str` | Template, Required | The shop's link name (current or former). |
| `body` | [`ApiShopsMatchPhotosRequest`](../../doc/models/api-shops-match-photos-request.md) | Body, Required | The colour option's values. |

## Response Type

**200**: A photo id for each colour Gemini could match. Colours it couldn't place are left out.

[`ApiShopsMatchPhotosResponse`](../../doc/models/api-shops-match-photos-response.md)

## Example Usage

```python
slug = 'vintageskates'

body = ApiShopsMatchPhotosRequest(
    colors=[
        Color(
            label='Cream',
            hex='#f3e9d2'
        ),
        Color(
            label='Red',
            hex='#b3261e'
        )
    ]
)

result = shops_api.match_color_photos(
    slug,
    body
)
print(result)
```

## Example Response *(as JSON)*

```json
{
  "matches": {
    "Cream": "LFRvGuTU3D8i334X",
    "Red": "SuqcgNv64HWN8H6e"
  }
}
```

## Errors

| HTTP Status Code | Error Description | Exception Class |
|  --- | --- | --- |
| 400 | Something in the request needs fixing; `error` says what. | [`ErrorResponseException`](../../doc/models/error-response-exception.md) |
| 404 | No such shop, or the admin token or API key doesn't match it. | [`ErrorResponseException`](../../doc/models/error-response-exception.md) |
| 429 | Over this network's cap for the call (see **Limits**). Retry after `Retry-After` seconds. | [`ErrorResponseException`](../../doc/models/error-response-exception.md) |
| 502 | Gemini, PayPal or Channel3 failed or isn't configured. | [`ErrorResponseException`](../../doc/models/error-response-exception.md) |


# Set Color Photos

Saves which photo shows each colour, and nothing else about the shop. Only colours already saved in the shop's options change; `null` clears a colour's photo. A photo id that isn't one of the shop's photos is ignored.

```python
def set_color_photos(self,
                    slug,
                    body)
```

## Authentication

This endpoint requires [AdminToken](../../doc/auth/custom-header-signature.md) **OR** [PlatformKey](../../doc/auth/oauth-2-bearer-token.md)

## Parameters

| Parameter | Type | Tags | Description |
|  --- | --- | --- | --- |
| `slug` | `str` | Template, Required | The shop's link name (current or former). |
| `body` | [`ApiShopsColorPhotosRequest`](../../doc/models/api-shops-color-photos-request.md) | Body, Required | The photo for each colour. |

## Response Type

**200**: The colours that were changed.

[`ApiShopsColorPhotosResponse`](../../doc/models/api-shops-color-photos-response.md)

## Example Usage

```python
slug = 'vintageskates'

body = ApiShopsColorPhotosRequest(
    photos={
        'Cream': 'LFRvGuTU3D8i334X',
        'Red': None
    }
)

result = shops_api.set_color_photos(
    slug,
    body
)
print(result)
```

## Example Response *(as JSON)*

```json
{
  "saved": [
    "Cream",
    "Red"
  ]
}
```

## Errors

| HTTP Status Code | Error Description | Exception Class |
|  --- | --- | --- |
| 400 | Something in the request needs fixing; `error` says what. | [`ErrorResponseException`](../../doc/models/error-response-exception.md) |
| 404 | No such shop, or the admin token or API key doesn't match it. | [`ErrorResponseException`](../../doc/models/error-response-exception.md) |


# Connect Pay Pal

Starts PayPal's seller onboarding (Partner Referrals). Send the seller's browser to the
returned `url`; they sign in to PayPal (or create a business account) and grant OneThing
permission. PayPal brings them back to `/api/shops/<slug>/paypal/return`, which saves the
connection and opens the manage page. From then on, sales are paid to that account.

Without a connection, a shop can still go live with a typed `paypal_email`.

**Platforms:** call it with your API key and a `returnUrl`, and PayPal's flow ends on your own
page instead, as `returnUrl?paypal=connected|incomplete|cancelled|failed&shop=<slug>`. The
URL's origin must be one registered on the key.

```python
def connect_pay_pal(self,
                   slug,
                   body=None)
```

## Authentication

This endpoint requires [AdminToken](../../doc/auth/custom-header-signature.md) **OR** [PlatformKey](../../doc/auth/oauth-2-bearer-token.md)

## Parameters

| Parameter | Type | Tags | Description |
|  --- | --- | --- | --- |
| `slug` | `str` | Template, Required | The shop's link name (current or former). |
| `body` | [`ApiShopsPaypalRequest`](../../doc/models/api-shops-paypal-request.md) | Body, Optional | Platform keys only: where PayPal sends the seller back. |

## Response Type

**200**: Where to send the seller.

[`ApiShopsPaypalResponse`](../../doc/models/api-shops-paypal-response.md)

## Example Usage

```python
slug = 'vintageskates'

body = ApiShopsPaypalRequest(
    return_url='https://www.miriogames.com/market/manage/?g=7Hq2'
)

result = shops_api.connect_pay_pal(
    slug,
    body=body
)
print(result)
```

## Example Response *(as JSON)*

```json
{
  "url": "https://www.sandbox.paypal.com/bizsignup/partner/entry?referralToken=EXAMPLE"
}
```

## Errors

| HTTP Status Code | Error Description | Exception Class |
|  --- | --- | --- |
| 404 | No such shop, or the admin token or API key doesn't match it. | [`ErrorResponseException`](../../doc/models/error-response-exception.md) |
| 502 | Gemini, PayPal or Channel3 failed or isn't configured. | [`ErrorResponseException`](../../doc/models/error-response-exception.md) |
| 503 | Gemini, PayPal or Channel3 failed or isn't configured. | [`ErrorResponseException`](../../doc/models/error-response-exception.md) |


# Get Pay Pal Connection

Asks PayPal where the seller's connection stands and saves it on the shop. Also finds a connection the seller finished at PayPal without coming back.

```python
def get_pay_pal_connection(self,
                          slug)
```

## Authentication

This endpoint requires [AdminToken](../../doc/auth/custom-header-signature.md) **OR** [PlatformKey](../../doc/auth/oauth-2-bearer-token.md)

## Parameters

| Parameter | Type | Tags | Description |
|  --- | --- | --- | --- |
| `slug` | `str` | Template, Required | The shop's link name (current or former). |

## Response Type

**200**: The connection, or nulls if there is none yet.

[`ApiShopsPaypalResponse1`](../../doc/models/api-shops-paypal-response-1.md)

## Example Usage

```python
slug = 'vintageskates'

result = shops_api.get_pay_pal_connection(slug)
print(result)
```

## Example Response *(as JSON)*

```json
{
  "merchantId": "7MZJ4QXN8K2LA",
  "status": {
    "receivable": true,
    "emailConfirmed": true,
    "checkedAt": "2026-10-21T18:04:11Z"
  }
}
```

## Errors

| HTTP Status Code | Error Description | Exception Class |
|  --- | --- | --- |
| 404 | No such shop, or the admin token or API key doesn't match it. | [`ErrorResponseException`](../../doc/models/error-response-exception.md) |
| 502 | Gemini, PayPal or Channel3 failed or isn't configured. | [`ErrorResponseException`](../../doc/models/error-response-exception.md) |
| 503 | Gemini, PayPal or Channel3 failed or isn't configured. | [`ErrorResponseException`](../../doc/models/error-response-exception.md) |


# Disconnect Pay Pal

Forgets the connected account. Sales go back to the shop's `paypal_email`.

```python
def disconnect_pay_pal(self,
                      slug)
```

## Authentication

This endpoint requires [AdminToken](../../doc/auth/custom-header-signature.md) **OR** [PlatformKey](../../doc/auth/oauth-2-bearer-token.md)

## Parameters

| Parameter | Type | Tags | Description |
|  --- | --- | --- | --- |
| `slug` | `str` | Template, Required | The shop's link name (current or former). |

## Response Type

**200**: Done.

[`Ok`](../../doc/models/ok.md)

## Example Usage

```python
slug = 'vintageskates'

result = shops_api.disconnect_pay_pal(slug)
print(result)
```

## Example Response *(as JSON)*

```json
{
  "ok": true
}
```

## Errors

| HTTP Status Code | Error Description | Exception Class |
|  --- | --- | --- |
| 404 | No such shop, or the admin token or API key doesn't match it. | [`ErrorResponseException`](../../doc/models/error-response-exception.md) |

