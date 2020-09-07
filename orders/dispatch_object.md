[1]:https://www.digital.iao.fraunhofer.de/de/publikationen/OpenTRANS21.html

## Dispatch Notification Object

The [OpenTRANS 2.1 specification][1] explains this object in detail.

### XML Example
```xml
<?xml version="1.0" encoding="UTF-8"?>
<DISPATCHNOTIFICATION>
  <DISPATCHNOTIFICATION_HEADER>
    <CONTROL_INFO>
      <GENERATION_DATE>2020-09-01T12:16:38</GENERATION_DATE>
    </CONTROL_INFO>
    <DISPATCHNOTIFICATION_INFO>
      <DISPATCHNOTIFICATION_ID>DNID0815</DISPATCHNOTIFICATION_ID>
      <DISPATCHNOTIFICATION_DATE>20200901</DISPATCHNOTIFICATION_DATE>
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
        <PARTY>
          <PARTY_ID/>
          <PARTY_ROLE>supplier</PARTY_ROLE>
          <ADDRESS>
            <NAME>JACOB Elektronik GmbH</NAME>
            <STREET>An der Roßweid 5</STREET>
            <ZIP>76229</ZIP>
            <CITY>Karlsruhe</CITY>
            <COUNTRY>Deutschland</COUNTRY>
            <COUNTRY_CODED>276</COUNTRY_CODED>
            <EMAIL>info@jacob.de</EMAIL>
          </ADDRESS>
        </PARTY>
      </PARTIES>
      <SHIPMENT_PARTIES_REFERENCE>
        <DELIVERY_IDREF>112233</DELIVERY_IDREF>
      </SHIPMENT_PARTIES_REFERENCE>
      <SHIPMENT_ID/>
      <TRACKING_TRACING_URL>&lt;![CDATA[]]&gt;</TRACKING_TRACING_URL>
    </DISPATCHNOTIFICATION_INFO>
  </DISPATCHNOTIFICATION_HEADER>
  <DISPATCHNOTIFICATION_ITEM_LIST>
    <DISPATCHNOTIFICATION_ITEM>
      <LINE_ITEM_ID>1</LINE_ITEM_ID>
      <PRODUCT_ID>
        <SUPPLIER_PID>47110815</SUPPLIER_PID>
        <BUYER_PID>999999999</BUYER_PID>
        <DESCRIPTION_SHORT>A really nice product</DESCRIPTION_SHORT>
      </PRODUCT_ID>
      <QUANTITY>2.00</QUANTITY>
      <ORDER_UNIT/>
      <ORDER_REFERENCE>
        <ORDER_ID>987654321</ORDER_ID>
        <LINE_ITEM_ID>1</LINE_ITEM_ID>
      </ORDER_REFERENCE>
      <SHIPMENT_PARTIES_REFERENCE>
        <DELIVERY_IDREF>112233</DELIVERY_IDREF>
      </SHIPMENT_PARTIES_REFERENCE>
    </DISPATCHNOTIFICATION_ITEM>
  </DISPATCHNOTIFICATION_ITEM_LIST>
  <DISPATCHNOTIFICATION_SUMMARY>
    <TOTAL_ITEM_NUM>2</TOTAL_ITEM_NUM>
  </DISPATCHNOTIFICATION_SUMMARY>
</DISPATCHNOTIFICATION>
```

### JSON Example
```json
{
  "dispatchNotificationHeader": {
    "generationDate": "2020-09-01T12:16:38",
    "dispatchNotificationInfo": {
      "dispatchNotificationId": "DNID0815",
      "dispatchNotificationDate": "20200901",
      "party": [
        {
          "partyId": "112233",
          "partyRole": "delivery",
          "address": {
            "name": "Max Mustermann",
            "street": "Musterstraße 123",
            "zip": "12345",
            "city": "Musterstadt",
            "country": "Deutschland",
            "countryCoded": "276",
            "email": "max@example.com",
            "phone": "01234567891"
          }
        },
        {
          "partyId": "112233",
          "partyRole": "buyer",
          "address": {
            "name": "Max Mustermann",
            "street": "Musterstraße 123",
            "zip": "12345",
            "city": "Musterstadt",
            "country": "Deutschland",
            "countryCoded": "276",
            "email": "max@example.com",
            "phone": "01234567891"
          }
        },
        {
          "partyId": "",
          "partyRole": "Supplier",
          "address": {
            "name": "JACOB Elektronik GmbH",
            "street": "An der Roßweid 5",
            "zip": "76229",
            "city": "Karlsruhe",
            "country": "Deutschland",
            "countryCoded": "276",
            "email": "info@jacob.de"
          }
        }
      ],
      "shipmentPartiesRef": {
        "deliveryIdRef": "112233"
      },
      "shipmentId": "",
      "trackingTracingUrl": "<![CDATA[]]>"
    }
  },
  "dispatchNotificationItemList": [
    {
      "lineItemId": "1",
      "productId": {
        "supplierPid": "47110815",
        "buyerPid": "999999999",
        "descriptionShort": "A really nice product"
      },
      "quantity": "2.00",
      "orderUnit": "",
      "orderRef": {
        "orderId": "987654321",
        "lineItemId": "1"
      },
      "shipmentPartiesRef": {
        "deliveryIdRef": "112233"
      }
    }
  ],
  "dispatchNotificationSummary": {
    "totalItemNum": "2"
  }
}
```
