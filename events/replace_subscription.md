## Replace a Subscription
Replace the specified [subscription](subscription_object.md) with the supplied one.

### Request
`PUT https://api.jacob.services/1.0/joe/events/subscriptions/{subscriptionId}`

| Header | Description | Supported Values |
| --- | --- | --- |
| `Content-Type` | MIME type of the subscription object | `application/json` |

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
# cat replacement.json
{
  "createdAt": "2020-09-02T15:40:33",
  "creator": "Mia Musterfrau",
  "event": "dispatch.generated",
  "identifier": {
    "type": "CustomerId",
    "value": "112233"
  },
  "webhook": {
    "url": "https://example.com/webhook",
    "authentication": {
      "type": "query",
      "queryParam": "token",
      "key": "3858f62230ac3c915f300c664312c63f"
    }
  }
}
# curl -X PUT -d @replacement.json https://api.jacob.services/1.0/joe/events/subscriptions/d8bbd7e0-f0df-11ea-adc1-0242ac120002
{
  "createdAt": "2020-09-02T15:40:33",
  "creator": "Mia Musterfrau",
  "event": "dispatch.generated",
  "identifier": {
    "type": "CustomerId",
    "value": "112233"
  },
  "webhook": {
    "url": "https://example.com/webhook",
    "authentication": {
      "type": "query",
      "queryParam": "token",
      "key": "3858f62230ac3c915f300c664312c63f"
    }
  },
  "subscriptionId": "d8bbd7e0-f0df-11ea-adc1-0242ac120002"
}
#
```
