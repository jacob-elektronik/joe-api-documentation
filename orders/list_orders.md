## List all Orders
Get a list of all orders. The default output format is JSON.

### Request
`GET https://api.jacob.services/1.0/joe`

| Header | Description | Supported Values |
| --- | --- | --- |
| `Accept` | Output format of the list | `*/*`, `application/json`, `application/xml` |

### Response
Returns a list of [links to orders](get_order.md).

| Status Code | Description |
| --- | --- |
| 200 | OK |
| 406 | Unsupported MIME type in `Accept` header |

### Example
```
# curl 'https://api.jacob.services/1.0/joe?apikey=123'
{
  "orderList": [
    "https://api.jacob.services/1.0/joe/987654319/order",
    "https://api.jacob.services/1.0/joe/987654320/order",
    "https://api.jacob.services/1.0/joe/987654321/order",
    "https://api.jacob.services/1.0/joe/987654322/order",
    "https://api.jacob.services/1.0/joe/987654323/order",
    "https://api.jacob.services/1.0/joe/987654324/order",
    "https://api.jacob.services/1.0/joe/987654325/order",
    "https://api.jacob.services/1.0/joe/987654326/order",
    "https://api.jacob.services/1.0/joe/987654327/order",
    "https://api.jacob.services/1.0/joe/987654328/order",
    "https://api.jacob.services/1.0/joe/987654329/order",
    "https://api.jacob.services/1.0/joe/987654330/order",
  ]
}
#
```