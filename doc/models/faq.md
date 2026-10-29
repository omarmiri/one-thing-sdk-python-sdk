
# Faq

One question and its answer.

## Structure

`Faq`

## Fields

| Name | Type | Tags | Description |
|  --- | --- | --- | --- |
| `q` | `str` | Required | The question. |
| `a` | `str` | Required | The answer. |

## Example

```python
from onethingapi.models.faq import Faq

faq = Faq(
    q='Are these suitable for outdoor skating?',
    a='Yes, on indoor rink floors and paved outdoor paths.'
)
```

