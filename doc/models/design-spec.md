
# Design Spec

What Gemini designed. OneThing's templates render it; Gemini never writes HTML.

## Structure

`DesignSpec`

## Fields

| Name | Type | Tags | Description |
|  --- | --- | --- | --- |
| `product_type` | [`ProductType2`](../../doc/models/product-type-2.md) | Required | - |
| `product_name` | `str` | Required | - |
| `layout` | [`Layout`](../../doc/models/layout.md) | Required | - |
| `palette` | [`Palette`](../../doc/models/palette.md) | Required | - |
| `fonts` | [`Fonts`](../../doc/models/fonts.md) | Required | - |
| `eyebrow` | `str` | Optional | - |
| `headline` | `str` | Required | - |
| `subheadline` | `str` | Optional | - |
| `story` | `str` | Optional | - |
| `bullets` | `List[str]` | Required | - |
| `details` | [`List[Detail]`](../../doc/models/detail.md) | Optional | - |
| `faq` | [`List[Faq]`](../../doc/models/faq.md) | Required | - |
| `cta_label` | `str` | Required | - |
| `suggested_price_usd` | `float` | Optional | - |
| `suggested_shipping_usd` | `float` | Optional | - |
| `image_alt` | `str` | Optional | - |
| `hero_prompt` | `str` | Optional | - |

## Example

```python
from onethingapi.models.design_spec import DesignSpec
from onethingapi.models.detail import Detail
from onethingapi.models.faq import Faq
from onethingapi.models.fonts import Fonts
from onethingapi.models.layout import Layout
from onethingapi.models.palette import Palette
from onethingapi.models.product_type_2 import ProductType2

design_spec = DesignSpec(
    product_type=ProductType2.DIGITAL,
    product_name='productName4',
    layout=Layout.MINIMAL,
    palette=Palette(
        background='#14171a',
        surface='#14171a',
        text='#14171a',
        muted='#14171a',
        accent='#14171a',
        accent_text='#14171a'
    ),
    fonts=Fonts(
        heading='heading2',
        body='body6'
    ),
    headline='headline4',
    bullets=[
        'bullets4',
        'bullets5'
    ],
    faq=[
        Faq(
            q='q0',
            a='a8'
        )
    ],
    cta_label='ctaLabel0',
    eyebrow='eyebrow0',
    subheadline='subheadline8',
    story='story0',
    details=[
        Detail(
            label='label0',
            value='value2'
        ),
        Detail(
            label='label0',
            value='value2'
        )
    ],
    suggested_price_usd=168.88
)
```

