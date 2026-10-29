# Files

Digital downloads and shop images.

```python
files_api = client.files
```

## Class Name

`FilesApi`

## Methods

* [Download File](../../doc/controllers/files.md#download-file)
* [Get Image](../../doc/controllers/files.md#get-image)


# Download File

A paid digital order's private link. Works 5 times within 14 days.

:information_source: **Note** This endpoint does not require authentication.

```python
def download_file(self,
                 token)
```

## Parameters

| Parameter | Type | Tags | Description |
|  --- | --- | --- | --- |
| `token` | `str` | Template, Required | The download token from a paid order's thank-you page. |

## Response Type

**200**: The file.

`binary`

## Example Usage

```python
token = 'q2Vd8mLx0RkT4nYb7HcW1sPe'

result = files_api.download_file(token)
print(result)
```

## Errors

| HTTP Status Code | Error Description | Exception Class |
|  --- | --- | --- |
| 410 | Expired or used up. | `ApiException` |


# Get Image

Public images only. Purchased files are never served here.

:information_source: **Note** This endpoint does not require authentication.

```python
def get_image(self,
             id)
```

## Parameters

| Parameter | Type | Tags | Description |
|  --- | --- | --- | --- |
| `id` | `str` | Template, Required | A shop's `photo_blob` or `hero_blob`. |

## Response Type

**200**: The image.

`Any`

## Example Usage

```python
id = 'LFRvGuTU3D8i334X'

result = files_api.get_image(id)
print(result)
```

## Errors

| HTTP Status Code | Error Description | Exception Class |
|  --- | --- | --- |
| 404 | Not a public shop image. | `ApiException` |

