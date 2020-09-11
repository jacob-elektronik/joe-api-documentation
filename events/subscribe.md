## Subscribe to an Event
Subscribe to an event by sending a [subscription object](subscription_object.md).

### Request
`POST https://api.jacob.services/1.0/joe/events/subscriptions`

| Header | Description | Supported Values |
| --- | --- | --- |
| `Content-Type` | MIME type of the subscription object | `application/json` |

### Response
Returns the request's subscription object with an additional `subscriptionId` field.

The `subscriptionId` can be used to [change](change_subscription.md) or [replace](replace_subscription.md) the subscription or to [unsubscribe](unsubscribe.md).

| Status Code | Description |
| --- | --- |
| 201 | Subscribed |
| 400 | An invalid subscription was sent |
| 415 | Unsupported media type |

### Example
```
# cat subscription.json
{
  "createdAt": "2020-09-01T12:17:02",
  "creator": "Max Mustermann",
  "event": "invoice.generated",
  "identifier": {
    "type": "CustomerId",
    "value": "112233"
  },
  "webhook": {
    "url": "https://example.com/webhook"
  }
}
# curl -d @subscription.json https://api.jacob.services/1.0/events/subscriptions
{
  "createdAt": "2020-09-01T12:17:02",
  "creator": "Max Mustermann",
  "event": "invoice.generated",
  "identifier": {
    "type": "CustomerId",
    "value": "112233"
  },
  "webhook": {
    "url": "https://example.com/webhook"
  },
  "subscriptionId": "d8bbd7e0-f0df-11ea-adc1-0242ac120002"
}
#
```
