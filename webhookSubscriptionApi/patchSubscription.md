# PATCH Subscription

---
Checks for update and if necessary, updates the existing subscription.
---

* This `curl` command checks for if there is need to update and then patches the subscription with the contents of user_patchsubscription.json. It updates an existing subscription.

```
Request:
curl -sS -X PATCH -H "Accept: application/json" -d @user_patchsubscription.json https://api.jacob.services/1.0/events/subscriptions/{subscriptionId}?apikey=abcdefghijklmnop
```

``` 
Responses:
    200 - OK, returns the newly updated subscription of the given subscriptionId
    400 - Bad request
    404 - Not found
```
--------------------------------------------------------------------------------------
Example response: Returns an updated subscription

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
