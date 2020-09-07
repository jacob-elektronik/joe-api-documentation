## Download an Order Response
Get the specified [order response](response_object.md). The default output format is XML.

### Request
`GET https://api.jacob.services/1.0/joe/{orderId}/response`

| URL Parameter | Description |
| --- | --- |
| `{orderId}` | Unique order number |

| Header | Description | Supported Values |
| --- | --- | --- |
| `Accept` | Output format of the list | `*/*`, `application/json`, `application/xml` |

### Response
Returns an [order response](response_object.md).

| Status Code | Description |
| --- | --- |
| 200 | OK |
| 204 | The requested document is not available |
| 406 | Unsupported MIME type in `Accept` header |

### Example
```
# curl https://api.jacob.services/1.0/joe/987654321/response?apikey=123
<?xml version="1.0" encoding="UTF-8"?>
<ORDERRESPONSE>
  <ORDERRESPONSE_HEADER>
    <ORDERRESPONSE_INFO>
      <ORDER_ID>987654321</ORDER_ID>
      <ORDERRESPONSE_DATE>20200901</ORDERRESPONSE_DATE>
      <SUPPLIER_ORDER_ID>OID0815</SUPPLIER_ORDER_ID>
      <PARTIES>
        <PARTY>
          <PARTY_ID>112233</PARTY_ID>
          <PARTY_ROLE>buyer</PARTY_ROLE>
          <ADDRESS>
            <NAME>Max Mustermann</NAME>
            <STREET>Musterstraße 123</STREET>
            <ZIP>12345</ZIP>
            <CITY>Musterstadt</CITY>
            <COUNTRY>Deutschland</COUNTRY>
            <COUNTRY_CODED>276</COUNTRY_CODED>
            <EMAIL>max@example.com</EMAIL>
            <PHONE>01234567891</PHONE>
          </ADDRESS>
        </PARTY>
        <PARTY>
          <PARTY_ID>112233</PARTY_ID>
          <PARTY_ROLE>delivery</PARTY_ROLE>
          <ADDRESS>
            <NAME>Max Mustermann</NAME>
            <STREET>Musterstraße 123</STREET>
            <ZIP>12345</ZIP>
            <CITY>Musterstadt</CITY>
            <COUNTRY>Deutschland</COUNTRY>
            <COUNTRY_CODED>276</COUNTRY_CODED>
            <EMAIL>max@example.com</EMAIL>
            <PHONE>01234567891</PHONE>
          </ADDRESS>
        </PARTY>
      </PARTIES>
      <ORDER_PARTIES_REFERENCE>
        <BUYER_IDREF>112233</BUYER_IDREF>
        <SUPPLIER_IDREF/>
      </ORDER_PARTIES_REFERENCE>
    </ORDERRESPONSE_INFO>
  </ORDERRESPONSE_HEADER>
  <ORDERRESPONSE_ITEM_LIST>
    <ORDERRESPONSE_ITEM>
      <LINE_ITEM_ID>1</LINE_ITEM_ID>
      <PRODUCT_ID>
        <SUPPLIER_PID>47110815</SUPPLIER_PID>
        <BUYER_PID>999999999</BUYER_PID>
        <DESCRIPTION_SHORT>A really nice product</DESCRIPTION_SHORT>
      </PRODUCT_ID>
      <QUANTITY>2</QUANTITY>
      <ORDER_UNIT>C62</ORDER_UNIT>
      <DELIVERY_DATE>
        <DELIVERY_START_DATE>2020-09-02</DELIVERY_START_DATE>
        <DELIVERY_END_DATE>2020-09-03</DELIVERY_END_DATE>
      </DELIVERY_DATE>
    </ORDERRESPONSE_ITEM>
  </ORDERRESPONSE_ITEM_LIST>
  <ORDERRESPONSE_SUMMARY>
    <TOTAL_ITEM_NUM>1</TOTAL_ITEM_NUM>
  </ORDERRESPONSE_SUMMARY>
</ORDERRESPONSE>
#
```