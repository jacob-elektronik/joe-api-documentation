## Get Document Status
Get the document status list for a specific order. The default output format is JSON.

### Request
`GET https://api.jacob.services/1.0/joe/{orderId}`

| URL Parameter | Description |
| --- | --- |
| `{orderId}` | Unique order number |

| Header | Description | Supported Values |
| --- | --- | --- |
| `Content-Type` | Output format of the list | `*/*`, `application/json`, `application/xml` |

### Response
Return a list of [documents](document_objects.md) and their availability for the specified order.

| Status Code | Description |
| --- | --- |
| 200 | OK |
| 400 | The supplied `{orderId}` was invalid |
| 406 | Unsupported MIME type in `Accept` header |

### Example
```
# curl https://api.jacob.services/1.0/joe/987654321\?apikey=123
{
  "order": {
    "link": "https://api.jacob.services/1.0/joe/987654321/order",
    "available": true
  },
  "response": {
    "link": "https://api.jacob.services/1.0/joe/987654321/response",
    "available": true
  },
  "invoice": {
    "link": "https://api.jacob.services/1.0/joe/987654321/invoice",
    "available": false
  },
  "dispatch": {
    "link": "https://api.jacob.services/1.0/joe/987654321/dispatch",
    "available": false
  }
}
#
```