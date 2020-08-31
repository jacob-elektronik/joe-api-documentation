# GET Subscription

---
retrieves a specific subscription with a subscriptionId.
---

* This `curl` command retrieves a specific subscription with a subscriptionId.

```
Request :
curl -sS -X GET -H "Accept: application/json"  https://api.jacob.services/1.0/events/subscriptions/{subscriptionId}?apikey=abcdefghijklmnop

```

``` 
Responses :
    200 - Ok, Returns a subscription with the given subscriptionId.
    400 - Bad Request.
    404 - Notfound.
```
--------------------------------------------------------------------------------------
Example Response for 200-Ok : Returns the subscription with the requested subscriptionId

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