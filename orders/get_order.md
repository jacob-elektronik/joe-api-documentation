## Download an Order
Get the specified [order](order_object.md). The default output format is XML.

### Request
`GET https://api.jacob.services/1.0/joe/{orderId}/order`

| URL Parameter | Description |
| --- | --- |
| `{orderId}` | Unique order number |

| Header | Description | Supported Values |
| --- | --- | --- |
| `Accept` | Output format of the list | `*/*`, `application/json`, `application/xml` |

### Response
Returns an [order](order_object.md).

| Status Code | Description |
| --- | --- |
| 200 | OK |
| 204 | The requested document is not available yet |
| 406 | Unsupported MIME type in `Accept` header |

### Example
```
# curl https://api.jacob.services/1.0/joe/987654321/order?apikey=123
<?xml version="1.0" encoding="UTF-8"?>
<ORDER>
  <ORDER_HEADER>
    <ORDER_INFO>
      <ORDER_ID>987654321</ORDER_ID>
      <ORDER_DATE>2020-08-10T10:05:37</ORDER_DATE>
      <LANGUAGE>ger</LANGUAGE>
      <PARTIES>
        <PARTY>
          <PARTY_ID>112233</PARTY_ID>
          <PARTY_ROLE>buyer</PARTY_ROLE>
          <ADDRESS>
            <NAME>Herr</NAME>
            <NAME2>Max Mustermann</NAME2>
            <STREET>Musterstraße 123</STREET>
            <ZIP>12345</ZIP>
            <CITY>Musterstadt</CITY>
            <COUNTRY>Deutschland</COUNTRY>
            <COUNTRY_CODED>DE</COUNTRY_CODED>
            <EMAIL>max@example.com</EMAIL>
          </ADDRESS>
        </PARTY>
        <PARTY>
          <PARTY_ID>998877</PARTY_ID>
          <PARTY_ROLE>supplier</PARTY_ROLE>
          <ADDRESS>
            <NAME>JACOB Elektronik GmbH</NAME>
            <STREET>An der Roßweid 5</STREET>
            <ZIP>76229</ZIP>
            <CITY>Karlsruhe</CITY>
            <COUNTRY>Deutschland</COUNTRY>
            <COUNTRY_CODED>DE</COUNTRY_CODED>
            <EMAIL>info@jacob.de</EMAIL>
          </ADDRESS>
        </PARTY>
        <PARTY>
          <PARTY_ID>112233</PARTY_ID>
          <PARTY_ROLE>delivery</PARTY_ROLE>
          <ADDRESS>
            <NAME>Herr</NAME>
            <NAME2>Max Mustermann</NAME2>
            <STREET>Musterstraße 123</STREET>
            <ZIP>12345</ZIP>
            <CITY>Musterstadt</CITY>
            <COUNTRY>Deutschland</COUNTRY>
            <COUNTRY_CODED>DE</COUNTRY_CODED>
            <EMAIL>max@example.com</EMAIL>
          </ADDRESS>
        </PARTY>
      </PARTIES>
      <CUSTOMER_ORDER_REFERENCE>
        <ORDER_ID>987654321</ORDER_ID>
      </CUSTOMER_ORDER_REFERENCE>
      <ORDER_PARTIES_REFERENCE>
        <BUYER_IDREF>112233</BUYER_IDREF>
        <SUPPLIER_IDREF>998877</SUPPLIER_IDREF>
      </ORDER_PARTIES_REFERENCE>
      <CURRENCY>EUR</CURRENCY>
    </ORDER_INFO>
  </ORDER_HEADER>
  <ORDER_ITEM_LIST>
    <ORDER_ITEM>
      <LINE_ITEM_ID>1</LINE_ITEM_ID>
      <PRODUCT_ID>
        <SUPPLIER_PID>47110815</SUPPLIER_PID>
        <BUYER_PID>999999999</BUYER_PID>
        <DESCRIPTION_SHORT>A really nice product</DESCRIPTION_SHORT>
      </PRODUCT_ID>
      <QUANTITY>2</QUANTITY>
      <ORDER_UNIT>C62</ORDER_UNIT>
      <PRODUCT_PRICE_FIX>
        <PRICE_AMOUNT>10.45</PRICE_AMOUNT>
      </PRODUCT_PRICE_FIX>
      <PRICE_LINE_AMOUNT>20.90</PRICE_LINE_AMOUNT>
    </ORDER_ITEM>
  </ORDER_ITEM_LIST>
  <ORDER_SUMMARY>
    <TOTAL_ITEM_NUM>1</TOTAL_ITEM_NUM>
    <TOTAL_AMOUNT>20.90</TOTAL_AMOUNT>
  </ORDER_SUMMARY>
</ORDER>
#
```