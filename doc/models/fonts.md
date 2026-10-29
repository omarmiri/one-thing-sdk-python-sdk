
# Fonts

Google Fonts for the page.

## Structure

`Fonts`

## Fields

| Name | Type | Tags | Description |
|  --- | --- | --- | --- |
| `heading` | `str` | Required | The headings font. |
| `body` | `str` | Required | The body text font. |

## Example

```python
from onethingapi.models.fonts import Fonts

fonts = Fonts(
    heading='Playfair Display',
    body='Inter'
)
```

