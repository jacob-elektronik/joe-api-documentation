[1]:https://www.digital.iao.fraunhofer.de/de/publikationen/OpenTRANS21.html

## Order Object

The [OpenTRANS 2.1 specification][1] explains this object in detail.

### XML Example
```xml
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
```

### JSON Example
```json
{
  "orderHeader": {
    "orderInfo": {
      "orderId": "987654321",
      "orderDate": "2020-08-10T10:05:37",
      "language": "ger",
      "parties": [
        {
          "partyId": "112233",
          "partyRole": "buyer",
          "address": {
            "name": "Herr",
            "name2": "Max Mustermann",
            "street": "Musterstraße 123",
            "zip": "12345",
            "city": "Musterstadt",
            "country": "Deutschland",
            "countryCoded": "DE",
            "email": "max@example.com"
          }
        },
        {
          "partyId": "998877",
          "partyRole": "supplier",
          "address": {
            "name": "JACOB Elektronik GmbH",
            "street": "An der Roßweid 5",
            "zip": "76229",
            "city": "Karlsruhe",
            "country": "Deutschland",
            "countryCoded": "DE",
            "email": "info@jacob.de"
          }
        },
        {
          "partyId": "112233",
          "partyRole": "delivery",
          "address": {
            "name": "Herr",
            "name2": "Max Mustermann",
            "street": "Musterstraße 123",
            "zip": "12345",
            "city": "Musterstadt",
            "country": "Deutschland",
            "countryCoded": "DE",
            "email": "max@example.com"
          }
        }
      ],
      "customerOrderRef": {
        "orderId": "987654321"
      },
      "orderPartiesRef": {
        "buyerIdRef": "112233",
        "supplierIdRef": "998877"
      },
      "currency": "EUR"
    }
  },
  "orderItemList": [
    {
      "lineItemId": "1",
      "productId": {
        "supplierPid": "47110815",
        "buyerPid": "999999999",
        "descriptionShort": "A really nice product"
      },
      "quantity": "2",
      "orderUnit": "C62",
      "productPriceFix": "10.45",
      "priceLineAmount": "20.90"
    }
  ],
  "orderSummary": {
    "totalItemNum": "1",
    "totalAmount": "20.90"
  }
}
```