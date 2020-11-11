## Product information
Get [product information](product_object.md) for a given SKU.

For products that are not in our portfolio anymore the call returns an empty object.

### Request
`GET https://api.jacob.services/1.0/products/{sku}`

| URL Parameter | Description |
| --- | --- |
| `{sku}` | The product's SKU |

### Response

| Status Code | Description |
| --- | --- |
| 200 | OK |
| 400 | The supplied `{sku}` was invalid |

### Example
```
# curl https://api.jacob.services/1.0/products/6252355
{
  "sku": 6252355,
  "shortDescription": "Xavax Eiswürfelform mit Deckel, für 36 Eiswürfel, 2er-Set (00111462)",
  "categoryID": 12616,
  "weight": 0,
  "condition": "new",
  "manufacturer": "Xavax",
  "ean": "4047443433374",
  "qty": 20,
  "deliveryTime": 1,
  "imageUrl": "https://d2zs7efolu1fdi.cloudfront.net/images/a6/f3/c7/6e/a6f3c76ef07513b6944cff51a29097f8.jpg"
}
#
```
