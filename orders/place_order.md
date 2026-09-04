## Place an Order
Place an [order](order_object.md). The input format is chosen via the `Content-Type` header; an unspecified or unknown value is treated as JSON.

### Request
`POST https://api.jacob.services/e-service/v1/orders`

| Header | Description | Supported Values |
| :--- | :--- | :--- |
| `apikey` | Your API key | |
| `Content-Type` | Input format of the order | `application/json`, `application/xml`, `text/xml` |

The request body is a complete [order object](order_object.md).

### Response
Returns an empty body. The JACOB order ID is **not** part of the response — [look it up by your own order number](get_order.md) once you need it.

| Status Code | Description |
| :--- | :--- |
| 201 | The order was placed |
| 400 | The order is invalid, or the request body could not be read. The response lists [every violation](../errors.md) |
| 401 | The API key is missing or invalid |
| 500 | Internal error |

A duplicate order number is reported as a `400` with the error code `DUPLICATE_ORDER`, not as a `409`. An order that was rejected earlier may be sent again under the same order number.

### Validation
The order is validated synchronously. All violations are collected and returned together in one `400` response, so work through the complete `details` list before sending again. See [errors](../errors.md) for the response format and the full list of codes.

These are the requirements JOE checks on the order itself:

**Order header**
* `orderID` — your own order number, set and not a placeholder (`0`, `null`, `nil`, `nill`, `empty` are rejected)
* `orderDate` — set, either `YYYY-MM-DD` or an RFC 3339 timestamp such as `2026-08-19T10:00:00+02:00`
* `currency` — set
* No allowances or charges — `payment.paymentTerms.timeForPayment[].allowOrChargesFix` must be empty
* No `jacob_SpecialArticle` header remark
* `UDX.WEBHOOK`, if present, must be a valid `https` URL — see [webhook delivery](../webhooks.md)

**Invoice recipient** — exactly one party with the role `invoice_recipient`
* One `partyID` of type `supplier_specific` carrying your master customer ID
* An address with `name2`, `street`, `zip`, `city` and `countryCoded`
* The address must match your invoice address in the JACOB customer master data. `name2`, `street`, `zip`, `city` and the resolved country code are compared; `DE` and `DEU` are treated as equal
* `countryCoded` must be a known ISO alpha-2 or alpha-3 country code

**Delivery party** — exactly one party with the role `delivery`, carrying exactly one address
* `name2`, `zip`, `city` and `countryCoded` must be set
* Minimum lengths: `name2` 3 characters, `zip` 2, `city` 1, `countryCoded` 2
* `countryCoded` must be a known ISO alpha-2 or alpha-3 country code

**Items** — at least one item, and per item
* `lineItemID` — set and unique within the order
* Exactly one article identifier, either a JACOB SKU or a GTIN (see below)
* `quantity` — a whole number of at least 1
* `productPriceFix.priceAmount` — greater than 0
* `priceLineAmount` — set, and exactly `quantity × priceAmount`
* Prices and amounts carry at most 2 decimal places
* The article must be orderable — internal process articles and 5-digit SKUs starting with `99` are rejected

**Order summary**
* `totalAmount` — greater than 0, and exactly the sum of all `priceLineAmount` values

Field lengths are listed with the [order object](order_object.md#field-lengths).

### Article Identification
Each item is identified by exactly one of two keys:

| Field | Requirement |
| :--- | :--- |
| `productID.supplierPid.value` (JACOB SKU) | numeric, at least 5 digits |
| `productID.internationalPid[]` with `type: gtin` | numeric, exactly 13 digits |

```json
// Option A: identification by JACOB SKU
"productID": {
  "supplierPid": { "value": "10000" }
}

// Option B: identification by GTIN-13, no supplierPid set
"productID": {
  "internationalPid": [
    { "type": "gtin", "value": "4012345678901" }
  ]
}
```

#### Notes
* If `supplierPid` is set, only the SKU is validated and used. A GTIN sent alongside it is then not used as an identifier.
* The GTIN is only evaluated when `supplierPid` is missing or empty.
* If neither key is present, the order is rejected with `MISSING_PRODUCT_IDENTIFIER`. A GTIN that is not numeric or not exactly 13 digits long yields `INVALID_GTIN`.
* The type comparison is not case-sensitive — `gtin`, `GTIN` and `Gtin` are equivalent.
* If an item carries several `internationalPid` entries of type `gtin`, the first one is used, even if a later one would be valid.
* The length limit of `internationalPid.value` applies to every entry, regardless of its type and regardless of whether a SKU is set. A value that is too long yields `FIELD_TOO_LONG`.

### Example
```
# cat order.json
{
  "orderHeader": {
    "orderInfo": {
      "orderID": "PO-TEST-001",
      "orderDate": "2026-08-19",
      "currency": "EUR",
      "parties": [
        {
          "partyRole": ["invoice_recipient"],
          "partyID": [
            { "type": "supplier_specific", "value": "112233" }
          ],
          "address": [
            {
              "name2": "Buyer GmbH",
              "street": "Hauptstr. 1",
              "zip": "12345",
              "city": "Berlin",
              "countryCoded": "DE"
            }
          ]
        },
        {
          "partyRole": ["delivery"],
          "address": [
            {
              "name2": "Wareneingang",
              "street": "Teststr. 1",
              "zip": "75175",
              "city": "Pforzheim",
              "countryCoded": "DE"
            }
          ]
        }
      ]
    }
  },
  "orderItemList": [
    {
      "lineItemID": "1",
      "quantity": 1,
      "productID": {
        "supplierPid": { "value": "10000" }
      },
      "productPriceFix": { "priceAmount": 10.00 },
      "priceLineAmount": 10.00
    }
  ],
  "orderSummary": {
    "totalAmount": 10.00,
    "totalItemNum": 1
  }
}

# curl
curl -X POST https://api.jacob.services/e-service/v1/orders \
  -H "apikey: 123" \
  -H "Content-Type: application/json" \
  -d @order.json

HTTP/1.1 201 Created
```

The invoice recipient's address in this example must be replaced with your own invoice address as held in the JACOB customer master data, and the `supplier_specific` party ID with your master customer ID.

The same order as OpenTRANS XML is sent with `Content-Type: application/xml`. See the [order object](order_object.md) for both representations.
