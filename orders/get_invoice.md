## Download an Invoice
Get the specified invoice. The default output format is XML.

### Request
`GET https://api.jacob.services/1.0/joe/{orderId}/invoice`

| URL Parameter | Description |
| --- | --- |
| `{orderId}` | Unique order number |

| Header | Description | Supported Values |
| --- | --- | --- |
| `Accept` | Output format of the list | `*/*`, `application/json`, `application/xml` |

### Response
Returns an [invoice](invoice_object.md).

| Status Code | Description |
| --- | --- |
| 200 | OK |
| 204 | The requested document is not available |
| 406 | Unsupported MIME type in `Accept` header |

### Example
```
# curl https://api.jacob.services/1.0/joe/987654321/invoice?apikey=123
<?xml version="1.0" encoding="UTF-8"?>
<INVOICE>
  <INVOICE_HEADER>
    <CONTROL_INFO>
      <GENERATION_DATE>2020-09-01T12:14:47</GENERATION_DATE>
    </CONTROL_INFO>
    <INVOICE_INFO>
      <INVOICE_ID>IID0815</INVOICE_ID>
      <INVOICE_DATE>20200901</INVOICE_DATE>
      <PARTIES>
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
      </PARTIES>
      <CURRENCY/>
    </INVOICE_INFO>
    <ORDER_HISTORY>
      <ORDER_ID>987654321</ORDER_ID>
      <SUPPLIER_ORDER_ID>OID0815</SUPPLIER_ORDER_ID>
    </ORDER_HISTORY>
  </INVOICE_HEADER>
  <INVOICE_ITEM_LIST>
    <INVOICE_ITEM>
      <LINE_ITEM_ID>1</LINE_ITEM_ID>
      <PRODUCT_ID>
        <SUPPLIER_PID>47110815</SUPPLIER_PID>
        <BUYER_PID>999999999</BUYER_PID>
        <DESCRIPTION_SHORT>A really nice product</DESCRIPTION_SHORT>
      </PRODUCT_ID>
      <QUANTITY>2.00</QUANTITY>
      <ORDER_UNIT>C62</ORDER_UNIT>
      <PRODUCT_PRICE_FIX>
        <PRICE_AMOUNT>10.45</PRICE_AMOUNT>
        <TAX_DETAILS_FIX>
          <TAX>0.00</TAX>
          <TAX_AMOUNT>3.34</TAX_AMOUNT>
        </TAX_DETAILS_FIX>
      </PRODUCT_PRICE_FIX>
      <PRICE_LINE_AMOUNT>24.24</PRICE_LINE_AMOUNT>
      <ORDER_REFERENCE>
        <ORDER_ID>987654321</ORDER_ID>
        <LINE_ITEM_ID>1</LINE_ITEM_ID>
      </ORDER_REFERENCE>
    </INVOICE_ITEM>
  </INVOICE_ITEM_LIST>
  <INVOICE_SUMMARY>
    <TOTAL_ITEM_NUM>1</TOTAL_ITEM_NUM>
    <NET_VALUE_GOODS>20.90</NET_VALUE_GOODS>
    <TOTAL_AMOUNT>24.24</TOTAL_AMOUNT>
    <ALLOW_OR_CHARGES_FIX>
      <ALLOW_OR_CHARGE type="surcharge">
        <ALLOW_OR_CHARGE_TYPE>freight</ALLOW_OR_CHARGE_TYPE>
        <ALLOW_OR_CHARGE_VALUE>
          <AOC_MONETARY_AMOUNT>0.00</AOC_MONETARY_AMOUNT>
        </ALLOW_OR_CHARGE_VALUE>
      </ALLOW_OR_CHARGE>
      <ALLOW_OR_CHARGES_TOTAL_AMOUNT>0.00</ALLOW_OR_CHARGES_TOTAL_AMOUNT>
    </ALLOW_OR_CHARGES_FIX>
    <TOTAL_TAX>
      <TAX_DETAILS_FIX>
        <TAX/>
        <TAX_AMOUNT>3.34</TAX_AMOUNT>
      </TAX_DETAILS_FIX>
    </TOTAL_TAX>
  </INVOICE_SUMMARY>
</INVOICE>
#
```