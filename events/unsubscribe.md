## Unsubscribe from an Event
Unsubscribe from the specified subscription.

### Request
`DELETE https://api.jacob.services/1.0/joe/events/subscriptions/{subscriptionId}`

### Response

| Status Code | Description |
| --- | --- |
| 200 | Unsubscribed |
| 404 | No such subscription |

### Example
```
# curl -X DELETE https://api.jacob.services/1.0/events/subscriptions/d8bbd7e0-f0df-11ea-adc1-0242ac120002
#
```
