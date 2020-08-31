# DELETE Subscription

---
Unsubscribe from events
---

* This `curl` command is used for unsubscribing/deleting a subscription.

```
Request:
curl -sS -X DELETE https://api.jacob.services/1.0/events/subscriptions/{subscriptionId}?apikey=abcdefghijklmnop
```

```
Responses:
    200 - OK, unsubscribed
    400 - Bad request
    404 - Not found
```
