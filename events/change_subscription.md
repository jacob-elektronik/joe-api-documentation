## Change a Subscription
Change the specified subscription by sending a partial [subscription](subscription_object.md).

### Request
`PATCH https://api.jacob.services/1.0/joe/events/subscriptions/{subscriptionId}`

| Header | Description | Supported Values |
| --- | --- | --- |
| `Content-Type` | MIME type of the subscription snippet | `application/json` |

### Response
Returns the changed subscription.

| Status Code | Description |
| --- | --- |
| 200 | OK |
| 400 | An invalid subscription snippet was sent |
| 404 | Subscription does not exist |
| 415 | Unsupported media type |

### Example
```
# cat add_basicauth.json
{
  "webhook": {
    "url": "https://example.com/webhook",
    "authentication": {
      "type": "basic",
      "user": "jacob_callback",
      "password": "3858f62230ac3c915f300c664312c63f"
    }
  }
}
# curl -X PATCH -d @add_basicauth.json https://api.jacob.services/1.0/joe/events/subscriptions/d8bbd7e0-f0df-11ea-adc1-0242ac120002
{
  "createdAt": "2020-09-01T12:17:08",
  "creator": "Max Mustermann",
  "event": "invoice.generated",
  "identifier": {
    "type": "CustomerId",
    "value": "112233"
  },
  "webhook": {
    "url": "https://example.com/webhook",
    "authentication": {
      "type": "basic",
      "user": "jacob_callback",
      "password": "3858f62230ac3c915f300c664312c63f"
    }
  },
  "subscriptionId": "d8bbd7e0-f0df-11ea-adc1-0242ac120002"
}
#
```
