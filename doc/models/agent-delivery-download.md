
# Agent Delivery Download

A digital file to download.

## Structure

`AgentDeliveryDownload`

## Fields

| Name | Type | Tags | Description |
|  --- | --- | --- | --- |
| `mtype` | `str` | Required, Constant | **Value**: `"download"` |
| `download_url` | `str` | Required | - |
| `note` | `str` | Optional | - |

## Example

```python
from onethingapi.models.agent_delivery_download import AgentDeliveryDownload

agent_delivery_download = AgentDeliveryDownload(
    download_url='download_url4',
    note='note0'
)
```

