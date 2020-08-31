# Create/Place order

---
Creates an order with the orderId of the user.
---

This is an example of a OpenTRANS XML document:

```xml
<?xml version="1.0" encoding="utf-8"?>
<ORDER>
	<ORDER_HEADER>
		<CONTROL_INFO>
			<GENERATION_DATE>2020-08-10T10:05:38</GENERATION_DATE>
		</CONTROL_INFO>
		<ORDER_INFO>
			<ORDER_ID>987654321</ORDER_ID>
			<ORDER_DATE>2020-08-10T10:05:37</ORDER_DATE>
			<LANGUAGE>ger</LANGUAGE>
			<PARTIES>
				<PARTY>
					<PARTY_ID>1234567</PARTY_ID>
					<PARTY_ROLE>buyer</PARTY_ROLE>
					<ADDRESS>
						<NAME>Herr</NAME>
						<NAME2>Max Mustermann</NAME2>
						<STREET>Musterstraße 123</STREET>
						<ZIP>12345</ZIP>
						<CITY>Musterstadt</CITY>
						<COUNTRY>Deutschland</COUNTRY>
						<COUNTRY_CODED>DE</COUNTRY_CODED>
						<EMAIL>someone@example.com</EMAIL>
					</ADDRESS>
				</PARTY>
				<PARTY>
					<PARTY_ID>556677</PARTY_ID>
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
					<PARTY_ID>1234567</PARTY_ID>
					<PARTY_ROLE>delivery</PARTY_ROLE>
					<ADDRESS>
						<NAME>Herr</NAME>
						<NAME2>Max Mustermann</NAME2>
						<STREET>Musterstraße 123</STREET>
						<ZIP>12345</ZIP>
						<CITY>Musterstadt</CITY>
						<COUNTRY>Deutschland</COUNTRY>
						<COUNTRY_CODED>DE</COUNTRY_CODED>
						<EMAIL>someone@example.com</EMAIL>
					</ADDRESS>
				</PARTY>
			</PARTIES>
			<CUSTOMER_ORDER_REFERENCE>
				<ORDER_ID>987654321</ORDER_ID>
			</CUSTOMER_ORDER_REFERENCE>
			<ORDER_PARTIES_REFERENCE>
				<BUYER_IDREF>112233</BUYER_IDREF>
				<SUPPLIER_IDREF>556677</SUPPLIER_IDREF>
			</ORDER_PARTIES_REFERENCE>
			<CURRENCY>EUR</CURRENCY>
		</ORDER_INFO>
	</ORDER_HEADER>
	<ORDER_ITEM_LIST>
		<ORDER_ITEM>
			<LINE_ITEM_ID>1</LINE_ITEM_ID>
			<PRODUCT_ID>
				<SUPPLIER_PID>430324</SUPPLIER_PID>
				<BUYER_PID>999999999</BUYER_PID>
				<DESCRIPTION_SHORT>Haselnusstafel</DESCRIPTION_SHORT>
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
------------------------------------------------------------------------------------------------------------

XML Definition : 

```xml
<ORDER_INFO>
    <ORDER_ID></ORDER_ID>
    <ORDER_DATE></ORDER_DATE>
    <LANGUAGE></LANGUAGE>
    <CURRENCY></CURRENCY>
    <CUSTOMER_ORDER_REFERENCE>
        <ORDER_ID></ORDER_ID>
    </CUSTOMER_ORDER_REFERENCE>
    <ORDER_PARTIES_REFERENCE>
        <BUYER_IDREF></BUYER_IDREF>
        <SUPPLIER_IDREF></SUPPLIER_IDREF>
    </ORDER_PARTIES_REFERENCE>
</ORDER_INFO>
```
------------------------------------------------------------------------------------------------------------

| XML Field | Description | More information | data type | example value |
| -------------- | :--------- | ----------:| ----------:|----------:| 
| &lt;ORDER_INFO&gt; |  administrative information on the order is summarized | - | - | - |
| &lt;ORDER_ID&gt; | The orderId of the user | - | string | 987654321 |
| &lt;ORDER_DATE&gt; | Date of the order  | format :yyyy-MM-dd'T'HH:mm:ss | date | 2020-08-10T10:05:38 |
| &lt;LANGUAGE&gt;  | Language | - | string | ger(german) |
| &lt;CURRENCY&gt;  | Currency information | - | string | EUR |
| &lt;CUSTOMER_ORDER_REFERENCE&gt;  |  related to an item and refers to the previous order where the item was ordered by the customer (purchasing party) | - | - | - |
| &lt;ORDER_ID&gt; |  Unique order number of the buyer/ orderId of the user  | Same as mentioned in the ORDER_INFO->ORDER_ID | string | 987654321 |
| &lt;ORDER_PARTIES_REFERENCE&gt;  |  related to an item and refers to the previous order where the item was ordered by the customer (purchasing party) | - | - | - |
| &lt;BUYER_IDREF&gt;  |  reference to the buyer|  The reference has to point to a (PARTY_ID) that is defined in the document (PARTY element buyer) | string | 112233 |
| &lt;SUPPLIER_IDREF&gt; | reference to the supplier| The reference has to point to a (PARTY_ID) that is defined in the document (PARTY element supplier) | string | 556677 |

------------------------------------------------------------------------------------------------------------

```xml
<ORDER_INFO>
    <PARTIES>
        <PARTY>
            <PARTY_ID></PARTY_ID>
            <PARTY_ROLE></PARTY_ROLE>
		<ADDRESS>
		    <NAME></NAME>
		    <NAME2></NAME2>
			<STREET></STREET>
			<ZIP></ZIP>
			<CITY></CITY>
			<COUNTRY></COUNTRY>
			<COUNTRY_CODED></COUNTRY_CODED>
			<EMAIL></EMAIL>
		</ADDRESS>
        </PARTY>
	</PARTIES>
</ORDER_INFO>
```
------------------------------------------------------------------------------------------------------------

| XML Field | Description | More information | data type | example value |
| -------------- | :--------- | ----------:| ----------:|----------:|
| &lt;PARTIES&gt; |  List of parties that are relevant to this business document | - | - | - |
| &lt;PARTY&gt; |   Information about a business partner | - | - | - |
| &lt;PARTY_ID&gt; |    Unique identifier ID of the business partner |  buyer_specific/customer_specific/supplier_specific  | string | 1234567 |
| &lt;PARTY_ROLE&gt; |     Role of the business partner in the context of this document | - | string | buyer/supplier/delivery |
| &lt;ADDRESS&gt; |     Address information of a business partner  | - | - | - |
| &lt;NAME&gt; |      Name of the organisation/salutation   | - | string | JACOB Elektronik GmbH/ Herr |
| &lt;NAME2&gt; |      Additional space for name   |  name of the specific individual | string | Max Mustermann |
| &lt;STREET&gt; |      Street name and house number  | - | string | Musterstraße 123 |
| &lt;ZIP&gt; |      ZIP code of address   | - | string | 12345 |
| &lt;CITY&gt; |       Town or city of the company   | - | string | Musterstadt |
| &lt;COUNTRY&gt; |       Country   | - | string | Deutschland |
| &lt;COUNTRY_CODED&gt; |       Code of the Country   | - | string | DE |
| &lt;EMAIL&gt; |       e-mail address   | - | string | someone@example.com |

------------------------------------------------------------------------------------------------------------

```xml
<ORDER_ITEM_LIST>
    <ORDER_ITEM>
        <LINE_ITEM_ID></LINE_ITEM_ID>
        <PRODUCT_ID>
            <SUPPLIER_PID></SUPPLIER_PID>
            <BUYER_PID></BUYER_PID>
            <DESCRIPTION_SHORT></DESCRIPTION_SHORT>
        </PRODUCT_ID>
        <QUANTITY></QUANTITY>
        <ORDER_UNIT></ORDER_UNIT>
        <PRODUCT_PRICE_FIX>
            <PRICE_AMOUNT></PRICE_AMOUNT>
        </PRODUCT_PRICE_FIX>
		<PRICE_LINE_AMOUNT></PRICE_LINE_AMOUNT>
    </ORDER_ITEM>
</ORDER_ITEM_LIST>
```

| XML Field | Description | More information | data type | example value |
| -------------- | :--------- | ----------:| ----------:|----------:|
| &lt;ORDER_ITEM_LIST&gt;  |  represents the lists of items in the order | - | - | - |
| &lt;ORDER_ITEM&gt;  | contains order information about exactly one item |  Any number of item lines can be used, although at least one item line must be used | - | - |
| &lt;LINE_ITEM_ID&gt;  |  The item ID number is used to uniquely identify the item line of an order within that order | - | string | 1 |
| &lt;PRODUCT_ID&gt;  |  Identifier of the product | - | - | - |
| &lt;SUPPLIER_PID&gt;  | Supplier's product ID | - | string | 430324 |
| &lt;BUYER_PID&gt;  | Product ID of the buying company  | - | string | 999999999 |
| &lt;DESCRIPTION_SHORT&gt;  | short description of the product | - | string | Haselnusstafel |
| &lt;QUANTITY&gt;  |  Quantity  | - | - | 2 |
| &lt;ORDER_UNIT&gt;  | Unit in which the product can be ordered | It is only possible to order multiples of the product unit. | string | C62 |
| &lt;PRODUCT_PRICE_FIX&gt;  |  A fixed product price  | - | - | - |
| &lt;PRICE_AMOUNT&gt;  |  Amount of the price of order item  | - | int | 10.45 |
| &lt;PRICE_LINE_AMOUNT&gt;  | The total price of the item-line | (PRICE_AMOUNT*QUANTITY) | int | 20.90 |

```
* PRICE_LINE_AMOUNT In the normal case the value results from multiplying  but has to be explicitly quoted. The element PRICE_LINE_ AMOUNT can result from multiplying PRICE_AMOUNT and PRICE_UNIT_VALUE if the price is not connected to the ordered unit but to another price-unit.
```
------------------------------------------------------------------------------------------------------------

```xml
<ORDER_SUMMARY>
    <TOTAL_ITEM_NUM></TOTAL_ITEM_NUM>
    <TOTAL_AMOUNT></TOTAL_AMOUNT>
</ORDER_SUMMARY>
```

| XML Field | Description | More information | data type | example value |
| -------------- | :--------- | ----------:| ----------:|----------:|
| &lt;ORDER_SUMMARY&gt;  | The summary contains information on the number of item lines in the order | This figure is used for control purposes to make sure that all items have been transferred | - | - |
| &lt;TOTAL_ITEM_NUM&gt;  |  Contains the total number of item lines in the business document | - | count | 1 |
| &lt;TOTAL_AMOUNT&gt;  |  Total amount covering all items in this business document.  | - | - | 20.90 |

  
- POST:
      consumes:
      - application/json
      - application/xml

* This `curl` command will create an Order in the CustomerOrder Api with the contents of the joe_order.user_order.xml : 

```
Request :
curl -vsS -X POST -H "Content-Type: application/xml" -d @joe_order.user_order.xml https://api.jacob.services/1.0/joe?apikey=9876

```

``` 
Responses :
    201 - Status created, for a successfully placed order.
    400 - Bad Request.
    409 - An order with this Id already exists.
```
--------------------------------------------------------------------------------------
Example Response : Returns the location of the placed order in the Response Header.

For a successfully placed order (201 Status Created), The response header contains the location of the placed order,  Location - https://api.jacob.services/1.0/joe/orderId/order, so the users can navigate to the particular location to take a look at their newly placed order.
