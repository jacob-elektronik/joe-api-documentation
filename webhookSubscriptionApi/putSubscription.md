# PUT Subscription

---
Replaces the complete existing subscription and updates it.
---

* This `curl` command replaces the whole subscription with the contents of user_updatesubscription.json, generally it updates the whole subscription.

```
Request :
curl -sS -X PUT -H "Accept: application/json" -d @user_updatesubscription.json https://api.jacob.services/1.0/events/subscriptions/{subscriptionId}?apikey=abcdefghijklmnop

```

``` 
Responses :
    200 - Ok, Returns the updated subscription of the given subscriptionId.
    400 - Bad Request.
    404 - Notfound.
```
--------------------------------------------------------------------------------------
Example Response for 200-Ok : Returns an Updated Subscription

```json
  {
    "createdAt": "string",
    "creator": "string",
    "event": "string",
    "identifier": {
      "type": "string",
      "value": "string"
    },
    "subscriptionId": "0268f288-7a76-4106-861f-bf1d1260b097",
    "webhook": {
      "authentication": {
        "header": "string",
        "key": "string",
        "password": "string",
        "queryParam": "string",
        "type": "string",
        "user": "string"
      },
      "url": "string"
    }
  }

```