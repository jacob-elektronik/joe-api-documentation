# Create/POST Subscription

---
Subscribe for events
---

* This `curl` command creates a subscription in the Subscription API with the contents of user_subscription.json
```
Request:
Headers required:
    Content-Type: application/json

curl -sS -X POST -H "Content-Type: application/json" -d @user_subscription.json  https://api.jacob.services/1.0/events/subscriptions/?apikey=abcdefghijklmnop
```

``` 
Responses:
    201 - Created, the response is the original subscription including a so-called subscriptionId.
    400 - Bad request
```
--------------------------------------------------------------------------------------
Example response: Returns the newly created subscription with its subscriptionId

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
