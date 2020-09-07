## Place an Order
Place an [order](order_object.md). The default input format is XML.

### Notes
`ORDER`.`ORDER_HEADER`.`ORDER_INFO`.`ORDER_ID` becomes the order ID. This order ID is referred to as `{orderId}` in other API calls.

Upon reception the following changes are made to the [order](order_object.md):
* `CUSTOMER_ORDER_REFERENCE`.`ORDER_ID` is set to the order ID.
* The buyer's `PARTY`.`PARTY_ID` is set to the customer's unique customer number here at JACOB.


### Request
`POST https://api.jacob.services/1.0/joe`

| Header | Description | Supported Values |
| --- | --- | --- |
| `Content-Type` | Input format of the order | `*/*`, `application/json`, `application/xml` |

### Response
Returns an empty body. The `Location` header of the response contains [a link to the placed order](get_order.md).

| Header | Description |
| --- | --- |
| Location | Link to the placed order |

| Status Code | Description |
| --- | --- |
| 201 | The order was placed |
| 400 | An invalid order was sent |
| 409 | An order with the specified order ID already exists |

### Example
```
# cat order.xml
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
# curl -d @order.xml https://api.jacob.services/1.0/joe/987654321?apikey=123
#
```
