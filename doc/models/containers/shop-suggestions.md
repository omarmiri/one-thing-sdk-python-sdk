
# Shop Suggestions

## Data Type

`Suggestions`

## Cases

| Type |
|  --- |
| [`Suggestions`](../../../doc/models/suggestions.md) |

## Suggestions

### Initialization Code

#### Example

```python
value = Suggestions(
    one_of_a_kind=False,
    options=[
        Option(
            name='Size',
            kind=Kind.SIZE,
            values=[
                OptionValue(
                    label='S'
                ),
                OptionValue(
                    label='M'
                ),
                OptionValue(
                    label='L'
                )
            ]
        )
    ],
    missing_facts=[
        MissingFact(
            label='Size',
            question='What size are the skates?',
            placeholder='US women\'s 8'
        )
    ]
)
```

