# GET documents

---
Retrieve documents related to a particular order with the given orderId.
---

* This `curl` command retrieves the specific document related to a particular order.

```
Document types: order, invoice, dispatch, response

Accept types: 
 - application/xml  - Returns XML document
 - application/json - Returns Json document

Request:
    curl -sS -X GET -H "Accept: application/xml" https://api.jacob.services/1.0/joe/orderId/documentType?apikey=9876
```

``` 
Responses:
    200 - OK, returns the XML document (Order/Invoice/Dispatch/Response)
    204 - The requested document is currently not available
    400 - Bad request
    406 - The request contained an unsupported 'Accept' header
```

--------------------------------------------------------------------------------------

* This `curl` command retrieves a list of available documents related to a particular order.

```
Request:
    curl -sS -X GET -H "Content-Type: application/json" "https://api.jacob.run/1.0/joe/orderId?apikey=9876"
```

``` 
Responses:
    200 - OK, returns a list of documents for the given orderId
    400 - Bad request
    406 - The request contained an unsupported 'Accept' header
```

--------------------------------------------------------------------------------------
Example Response: Returns a list of links to all available documents for this order.

```
{
  "order": {
    "link": "https://api.jacob.services/1.0/joe/orderId/order",
    "available": true
  },
  "response": {
    "link": "https://api.jacob.services/1.0/joe/orderId/response",
    "available": true
  },
  "invoice": {
    "link": "https://api.jacob.services/1.0/joe/orderId/invoice",
    "available": false
  },
  "dispatch": {
    "link": "https://api.jacob.services/1.0/joe/orderId/dispatch",
    "available": false
  }
}
```
