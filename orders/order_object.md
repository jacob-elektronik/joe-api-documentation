[1]:https://www.digital.iao.fraunhofer.de/de/publikationen/OpenTRANS21.html

## Order Object

The [OpenTRANS 2.1 specification][1] explains this object in detail. This page shows the JSON and XML representations JOE 2.0 accepts, and the constraints it enforces. The complete schema is available in the [Swagger documentation](https://api.jacob.services/e-service/v1/docs/index.html).

Both examples below are the same minimal, valid order: one item, identified by JACOB SKU.

### JSON Example
```json
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
              "name": "Buyer GmbH",
              "name2": "Max Mustermann",
              "street": "Hauptstr. 1",
              "zip": "12345",
              "city": "Berlin",
              "countryCoded": "DE",
              "email": "max@example.com",
              "vatID": "DE999999999"
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
      ],
      "headerUDX": {
        "UDX.WEBHOOK": "https://your-server.example.com/jacob-webhook"
      }
    }
  },
  "orderItemList": [
    {
      "lineItemID": "1",
      "productID": {
        "supplierPid": { "value": "10000" },
        "descriptionShort": "Test article"
      },
      "quantity": 1,
      "orderUnit": "C62",
      "productPriceFix": { "priceAmount": 10.00 },
      "priceLineAmount": 10.00
    }
  ],
  "orderSummary": {
    "totalItemNum": 1,
    "totalAmount": 10.00
  }
}
```

### XML Example
```xml
<?xml version="1.0" encoding="UTF-8"?>
<ORDER xmlns="http://www.opentrans.org/XMLSchema/2.1" type="standard" version="2.1">
  <ORDER_HEADER>
    <ORDER_INFO>
      <ORDER_ID>PO-TEST-001</ORDER_ID>
      <ORDER_DATE>2026-08-19</ORDER_DATE>
      <PARTIES>
        <PARTY>
          <PARTY_ID type="supplier_specific">112233</PARTY_ID>
          <PARTY_ROLE>invoice_recipient</PARTY_ROLE>
          <ADDRESS>
            <NAME>Buyer GmbH</NAME>
            <NAME2>Max Mustermann</NAME2>
            <STREET>Hauptstr. 1</STREET>
            <ZIP>12345</ZIP>
            <CITY>Berlin</CITY>
            <COUNTRY_CODED>DE</COUNTRY_CODED>
            <EMAIL>max@example.com</EMAIL>
            <VAT_ID>DE999999999</VAT_ID>
          </ADDRESS>
        </PARTY>
        <PARTY>
          <PARTY_ROLE>delivery</PARTY_ROLE>
          <ADDRESS>
            <NAME2>Wareneingang</NAME2>
            <STREET>Teststr. 1</STREET>
            <ZIP>75175</ZIP>
            <CITY>Pforzheim</CITY>
            <COUNTRY_CODED>DE</COUNTRY_CODED>
          </ADDRESS>
        </PARTY>
      </PARTIES>
      <CURRENCY>EUR</CURRENCY>
      <HEADER_UDX>
        <UDX.WEBHOOK>https://your-server.example.com/jacob-webhook</UDX.WEBHOOK>
      </HEADER_UDX>
    </ORDER_INFO>
  </ORDER_HEADER>
  <ORDER_ITEM_LIST>
    <ORDER_ITEM>
      <LINE_ITEM_ID>1</LINE_ITEM_ID>
      <PRODUCT_ID>
        <SUPPLIER_PID>10000</SUPPLIER_PID>
        <DESCRIPTION_SHORT>Test article</DESCRIPTION_SHORT>
      </PRODUCT_ID>
      <QUANTITY>1</QUANTITY>
      <ORDER_UNIT>C62</ORDER_UNIT>
      <PRODUCT_PRICE_FIX>
        <PRICE_AMOUNT>10.00</PRICE_AMOUNT>
      </PRODUCT_PRICE_FIX>
      <PRICE_LINE_AMOUNT>10.00</PRICE_LINE_AMOUNT>
    </ORDER_ITEM>
  </ORDER_ITEM_LIST>
  <ORDER_SUMMARY>
    <TOTAL_ITEM_NUM>1</TOTAL_ITEM_NUM>
    <TOTAL_AMOUNT>10.00</TOTAL_AMOUNT>
  </ORDER_SUMMARY>
</ORDER>
```

### Notes
* `orderInfo.orderID` (`ORDER_ID`) is your own order number. Use it as the `customerOrderID` to [look up the JACOB order ID](get_order.md).
* `orderDate` accepts `YYYY-MM-DD` as well as RFC 3339 timestamps, e.g. `2026-08-19T10:00:00+02:00`.
* The validated country field is `countryCoded` (`COUNTRY_CODED`), not `country`. It takes an ISO alpha-2 or alpha-3 code.
* `name` (`NAME`) carries the company name or a salutation, `name2` (`NAME2`) the actual name. `name2` is the field JOE validates and compares against your master data, so it must be set on both the invoice recipient and the delivery address. If `name2` is empty and `name3` is set, `name3` is promoted to `name2`.
* Leading and trailing characters that are neither letters nor digits are trimmed from the address fields before they are validated and compared.
* `vatID` (`VAT_ID`) of the invoice recipient is used in the tax calculation process. It must be provided for orders eligible for tax exemption.
* `priceLineAmount` must be exactly `quantity × productPriceFix.priceAmount`, and `orderSummary.totalAmount` exactly the sum of all `priceLineAmount` values. Both carry at most 2 decimal places.
* `headerUDX` (`HEADER_UDX`) is a flat set of key/value fields. `UDX.WEBHOOK` is the only one you set yourself and it is optional — see [webhook delivery](../webhooks.md). Any `UDX.JACOB.*` field in an incoming order is dropped; those are set by JACOB.
* Upon reception `customerOrderReference.orderID` is set to your order number, and the JACOB order ID is stored in `headerUDX` — it is returned as `UDX.JACOB.EXTERNAL.ORDER_ID` in XML and as `nomOrderID` in JSON.

### Field Lengths
Exceeding one of these limits yields the error code `FIELD_TOO_LONG`; the message names the field. Lengths are counted in characters.

| Field | Max length |
| :--- | :--- |
| `orderHeader.orderInfo.orderID` | 250 |
| `orderHeader.orderInfo.currency` | 3 |
| `address.name`, `address.name2`, `address.name3` | 50 |
| `address.street`, `address.city`, `address.country` | 50 |
| `address.zip` | 20 |
| `address.vatID` | 50 |
| `address.email` | 255 |
| `orderItemList[].lineItemID` | 50 |
| `orderItemList[].orderUnit` | 3 |
| `productID.supplierPid.value` | 32 |
| `productID.internationalPid[].value` | 50 |
| `productID.descriptionShort` | 150 |

The delivery address additionally has minimum lengths — `name2` 3 characters, `zip` 2, `city` 1, `countryCoded` 2. Falling below one of them yields `DELIVERY_ADDRESS_FIELD_TOO_SHORT`.
