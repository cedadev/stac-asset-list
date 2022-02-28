# stac-asset-list
API extension to add `/collections/<collectionId>/items/<itemId>/assets` url


|   |   |
|---|---|
| **OpenAPI Specification** | [openapi.yaml](openapi.yaml) |
| **Conformance Class** | https://api.stacspec.org/v1.0.0-beta.5/asset-list |
| **[Maturity Classification](https://github.com/radiantearth/stac-api-spec/blob/master/extensions.md#extension-maturity)** | Pilot |

There may be cases where the number of assets per item exceeds the number which can be 
reasonably returned as a nested object. This extension provides the implementation to
allow you to link to a paginated list of assets from item objects, thus reducing the 
number of objects in the item-search response.

It is recommended to keep the metadata assets as a nested object in the `assets` key of the [item
specification](https://github.com/radiantearth/stac-spec/blob/master/item-spec/item-spec.md#assets). These
are useful for clients and provide links to thumbnails and other metadata which would be useful during the
browsing process.

Implementing this link should be within the [link object](https://github.com/radiantearth/stac-spec/blob/master/item-spec/item-spec.md#link-object)
from the item using the relation `asset`.

This should be implemented with some form of pagination to allow scrolling of the asset list.

## Examples

* [Item example](examples/item.json)
* [Asset Response](https://github.com/cedadev/stac-asset-spec/blob/main/examples/simple-asset.json)

### HTTP GET Example

Request:
```http
HTTP GET /colletions/<collectionID>/items/<itemID>/assets
```

Response with `200 OK`:
```json
{
    "type": "FeatureCollection",
    "features": [],
    "links": [
        {
            "rel": "next",
            "href": "http://api.cool-sat.com/search?page=2"
        }
    ]
}
```

## HTTP POST Example

Request:
```json
{
    "bbox": [-110, 39.5, -105, 40.5],
    "limit": 10
}
```

Response with `200 OK`:
```json
{
    "type": "FeatureCollection",
    "features": [],
    "links": [
        {
            "rel": "next",
            "href": "http://api.cool-sat.com/search?page=2"
        }
    ]
}
```
