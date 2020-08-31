A basic subscription looks like this: 
```json
{
  "event": "invoice.generated",
  "creator": "M. Mustermann",
  "identifier": {
    "type": "customerId",
    "value": "4711"
  },
  "webhook": {
    "url": "https://example.com/webhook"
  }
}
```

Subscription with authentication type 'basic':
```json
{
  "event": "invoice.generated",
  "creator": "M. Mustermann",
  "identifier": {
    "type": "customerId",
    "value": "4711"
  },
  "webhook": {
    "url": "https://example.com/webhook",
    "authentication": {
      "type": "basic",
      "user": "foo",
      "password": "baa"
    }
  }
}
```

Subscription with authentication type 'header':
```json
{
  "event": "invoice.generated",
  "creator": "M. Mustermann",
  "identifier": {
    "type": "customerId",
    "value": "4711"
  },
  "webhook": {
    "url": "https://example.com/webhook",
    "authentication": {
      "type": "header",
      "header": "x-api-key",
      "key": "secretToken12345"
    }
  }
}
```

Subscription with Webhook Authentication type 'queryParam':
```json
{
  "event": "invoice.generated",
  "creator": "M. Mustermann",
  "identifier": {
    "type": "customerId",
    "value": "4711"
  },
  "webhook": {
    "url": "https://example.com/webhook",
    "authentication": {
      "type": "queryParam",
      "queryParam": "apikey",
      "key": "secretToken09876"
    }
  }
}
```
 
```
* event          - It is the event on which the user wants to subscribe for.
* creator        - Name of the creator.
* identifier     - Identifier has a type, which can be a customerId or an orderId and its corresponding value.
* webhook        - URL here is the user's endpoint, which they want to register and this URL gets notified whenever there is a change in the state of the order, depending on the events which the user subscribed to.
```
