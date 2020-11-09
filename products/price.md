## Price Information
Get [price information](price_object.md) for a given SKU.

This API endpoint is public, it does not require authentication.

### Request
`GET https://api.jacob.services/1.0/products/{sku}/price`

| URL Parameter | Description |
| --- | --- |
| `{sku}` | The product's SKU |

### Response

| Status Code | Description |
| --- | --- |
| 200 | OK |
| 404 | The supplied `{sku}` was either invalid or the product is not in our portfolio anymore |

### Example
```
# curl https://api.jacob.services/1.0/products/6252355/price
{
  "sku": 6252355,
  "net": 10.4,
  "qty": 20,
  "currency": "EUR"
}
#
```
