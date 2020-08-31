# GET Subscriptions

---
Retrieves a list of subscriptions of a user with specific event and identifier.
---

* This `curl` command retrieves a list of subscriptions of a user with specific event and identifier..

```
Request :
curl -sS -X GET -H "Accept: application/json"  https://api.jacob.services/1.0/events/subscriptions?event=example.event&identifierType=exampleId&identifierValue=exampleValue&apikey=abcdefghijklmnop

```

``` 
Responses :
    200 - Ok, Return a list of all the subscriptions of a user.
    400 - Bad Request.
    404 - Notfound.
```
--------------------------------------------------------------------------------------
Example Response for 200-Ok: Returns a list of subscriptions with the given Event and Identifier.

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