# GET documents

---
Retrieves the different documents related to a particular order with the given orderId.
---

* This curl command retrieves the specific document related to a particular order.

```
Document types : Order, Invoice, Dispatch, Response.

Accept types : 
 - application/xml  - Returns XML document.
 - application/json - Returns Json document.

Request :
    curl -sS -X GET -H "Accept: application/xml" https://api.jacob.services/1.0/joe/orderId/documentType?apikey=9876

```

``` 
Responses :
    200 - Ok, Returns the XML document (Order/Invoice/Dispatch/Response).
    204 - The requested document is currently not available.
    400 - Bad Request.
    406 - The request contained an unsupported 'Accept' header.
```

--------------------------------------------------------------------------------------

* This curl command retrieves a list of available documents related to a particular order.

```
Request :
    curl -sSX GET -H "Content-Type: application/json" "https://api.jacob.run/1.0/joe/orderId?apikey=9876"
```

``` 
Responses :
    200 - Ok, Returns a list of documents for the given orderId.
    400 - Bad Request.
    406 - The request contained an unsupported 'Accept' header.
```

--------------------------------------------------------------------------------------
Example Response : Returns a list of links with locations for all the available documents.


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