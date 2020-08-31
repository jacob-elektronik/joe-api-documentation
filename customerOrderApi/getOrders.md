# GET orders

---
Retrieve a list of orders
---

* This `curl` command will retrieve a list of orders.

```
Request:

Accept types: 
 - application/xml  - Returns a list of XML orders.
 - application/json - Returns a list of JSON orders.

curl -sS -X GET -H "Accept: application/xml" https://api.jacob.services/1.0/joe?apikey=9876

curl -sS -X GET -H "Accept: application/json"  https://api.jacob.services/1.0/joe?apikey=9876
```

``` 
Responses:
    200 - OK, returns a list of orders
    400 - Bad request
    406 - The request contained an unsupported 'Accept' header
```
--------------------------------------------------------------------------------------
Example response: Returns a list of links to all available orders.

```
{
  "orderList": [
    "https://api.jacob.services/1.0/joe/{orderId}/order",
    "https://api.jacob.services/1.0/joe/{orderId}/order",
    "https://api.jacob.services/1.0/joe/{orderId}/order",
    "https://api.jacob.services/1.0/joe/{orderId}/order"
  ]
}
```
