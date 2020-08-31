A Subscription looks like this : 

 ```json
 {
  "event": "invoice.generated",
  "creator": "4711|tool|manual",
  "identifier": {
       "type": "customerId",
       "value": "4711"
   },
   "webhook": {
       "url": "https://example.customerendpoint.com/webhook"
   }
}
 ```

Subscription with Webhook Authentication type basic :
```json
{
  "event": "invoice.generated",
  "creator": "4711|tool|manual",
  "identifier": {
       "type": "customerId",
       "value": "4711"
   },
   "webhook": {
       "url": "https://example.customerendpoint.com/webhook",
       "authentication": {
           "type" : "basic",
           "user" : "foo",
           "password": "baa",
       }
   }
}
```

Subscription with Webhook Authentication type header :
```json
{
  "event": "invoice.generated",
  "creator": "4711|tool|manual",
  "identifier": {
       "type": "customerId",
       "value": "4711"
   },
   "webhook": {
       "url": "https://example.customerendpoint.com/webhook",
       "authentication": {
           "type" : "header",
           "header" : "x-api-key",
           "key": "fooBaa4711Lulu",
       }
   }
}
```

Subscription with Webhook Authentication type queryParam :
```json
{
  "event": "invoice.generated",
  "creator": "4711|tool|manual",
  "identifier": {
       "type": "customerId",
       "value": "4711"
   },
   "webhook": {
       "url": "https://example.customerendpoint.com/webhook",
       "authentication": {
           "type" : "queryParam",
           "queryParam" : "apikey",
           "key": "fooBaa4711Lulu",
       }
   }
}
```
 
```
* event          - It is the event on which the user wants to subscribe for.
* creator        - name of the creator.
* identifier     - Identifier has a type, which can be a customerId or an orderId and its corresponding value.
* webhook        - url here is the user's endpoint, which they want to register and this url gets notified whenever there is a change in the state of the order , depending on the events which the user subscribed to.

```