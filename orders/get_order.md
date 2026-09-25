## Get an Order
An order can be fetched in two ways: by your own order number, or by the JACOB order ID.

Placing an order does not return the JACOB order ID, so start with your own order number to resolve it.

### Look up an Order by your own Order Number
`GET https://api.jacob.services/e-service/v1/orders?customerOrderID={id}`

| Parameter | Description |
| :--- | :--- |
| `customerOrderID` | The `orderHeader.orderInfo.orderID` you sent when [placing the order](place_order.md) |

### Download an Order
`GET https://api.jacob.services/e-service/v1/orders/{orderID}`

| Parameter | Description |
| :--- | :--- |
| `orderID` | The JACOB order ID, `JE` followed by digits, e.g. `JE912345671000` |

### Response
Returns the [order](order_object.md) as JSON. The JACOB order ID is part of the header UDX fields:

```json
{
  "orderHeader": {
    "orderInfo": {
      "orderID": "PO-TEST-001",
      "headerUDX": {
        "nomOrderID": { "String": "JE912345671000", "Valid": true },
        "customerOrderID": "PO-TEST-001",
        "masterCustomerID": "112233",
        "importState": "imported"
      }
    }
  }
}
```

`nomOrderID` is a nullable string, so read it from its `String` member. It stays empty until JACOB has assigned the order ID — keep polling until it is set.

`importState` reports how far the order got in the JACOB import: `pending`, `imported`, `rejected` or `parked`.

| Status Code | Description |
| :--- | :--- |
| 200 | The order was found |
| 400 | `customerOrderID` is missing, or `orderID` is not in the format `JE` followed by digits |
| 401 | The API key is missing or invalid |
| 404 | No such order |
| 500 | Internal error |

Orders of other customers are not visible: requesting one yields a `404`, not a `403`.

### Example
```
curl "https://api.jacob.services/e-service/v1/orders?customerOrderID=PO-TEST-001" \
  -H "apikey: 123"

curl "https://api.jacob.services/e-service/v1/orders/JE912345671000" \
  -H "apikey: 123"
```
