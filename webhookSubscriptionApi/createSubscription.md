# Create/POST Subscription

---
Creates a subscription
---

* This `curl` command creates a subscription in the Subscription Api with the contents of user_subscription.json
```
Request :
Headers required - 
    Content-Type : application/json

curl -sS -X POST -H "Content-Type: application/json" -d @user_subscription.json  https://api.jacob.services/1.0/events/subscriptions/?apikey=abcdefghijklmnop

```

``` 
Responses :
    201 - Status created, for a successful subscription, meaning a user has successfully subscribed to an event. Also gives the user a subscriptionId which can be used later.
    400 - Bad Request.
```
--------------------------------------------------------------------------------------
Example Response for a successful subscription 201-Status created : Returns the newly created subscription

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