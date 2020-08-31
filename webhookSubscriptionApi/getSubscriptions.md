# GET Subscriptions

---
Retrieve a list of subscriptions for a specific event/identifier combination.
---

* This `curl` command retrieves a list of subscriptions for the specific event and identifier.

```
Request:
curl -sS -X GET -H "Accept: application/json"  https://api.jacob.services/1.0/events/subscriptions?event=example.event&identifierType=exampleId&identifierValue=exampleValue&apikey=abcdefghijklmnop
```

``` 
Responses:
    200 - OK, return a list of all subscriptions
    400 - Bad request
    404 - Not found
```
--------------------------------------------------------------------------------------
Example Response: Returns a list of subscriptions with the given event and identifier.

```json
[
  {
    "createdAt": "string",
    "creator": "string",
    "event": "string",
    "identifier": {
      "type": "string",
      "value": "string"
    },
    "subscriptionId": "string",
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
]
```
