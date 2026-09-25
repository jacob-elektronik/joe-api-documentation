## Errors

### HTTP Status Codes
| Status | Meaning |
| :--- | :--- |
| 201 Created | The order was accepted — without a response body |
| 400 Bad Request | Validation error (with a `details` list) or an unreadable request body |
| 401 Unauthorized | The API key is missing or invalid |
| 404 Not Found | No such order — generic message, no error code |
| 429 Too Many Requests | The [rate limit](README.md#rate-limits) was exceeded. This comes from the API gateway and carries no JOE error code |
| 500 Internal Server Error | Internal error |

The API returns neither `403` nor `409`. An order of another customer yields a `404`, and a duplicate order number a `400` with the error code `DUPLICATE_ORDER`.

**A document that does not exist yet is not an error.** `/responses`, `/dispatches` and `/invoices` answer `200` with an empty list as long as no document exists — keep polling, do not wait for a `404`.

### Error Response Format
```json
{
  "error": "invalid order",
  "details": [
    {
      "code": "INVALID_LINE_AMOUNT",
      "message": "PriceLineAmount calculation mismatch. Actual: '30.02', expected: '30.03' (LineItem: 1)",
      "position": 1,
      "lineItemID": "1"
    },
    {
      "code": "MISSING_CURRENCY",
      "message": "currency must be set"
    }
  ]
}
```

* **All violations are collected** — one response can hold several `details` entries, not just the first violation.
* `position` (1-based) and `lineItemID` are only set for item-related violations, otherwise they are `0` and empty.
* Item-related `message` texts carry the suffix `(LineItem: <id>)`.
* Only validation errors (`400`) publish `details`. All other errors return the generic `error` message alone.
* **Evaluate `code`, not `message`** — the message texts are not part of the contract.

### Validation Error Codes

#### Order Header
| Code | Meaning |
| :--- | :--- |
| `INVALID_CUSTOMER_ORDER_ID` | `orderHeader.orderInfo.orderID` is missing or a placeholder (`0`, `null`, `nil`, `nill`, `empty`) |
| `DUPLICATE_ORDER` | An order with this `orderID` already exists. An order that was rejected earlier may be sent again under the same ID |
| `MISSING_ORDER_DATE` | The order date is not set |
| `MISSING_CURRENCY` | The currency is not set |
| `UNSUPPORTED_ALLOW_OR_CHARGES` | Allowances and charges are not supported |
| `INVALID_REMARK` | A `jacob_SpecialArticle` remark is not accepted |
| `INVALID_WEBHOOK_URL` | The webhook URL in the UDX field `UDX.WEBHOOK` is not a valid `https` URL — see [webhook delivery](webhooks.md) |

#### Invoice Recipient
| Code | Meaning |
| :--- | :--- |
| `MISSING_INVOICE_RECIPIENT` | No party with the role `invoice_recipient` |
| `TOO_MANY_INVOICE_RECIPIENTS` | More than one `invoice_recipient` party |
| `INVALID_INVOICE_RECIPIENT` | The `supplier_specific` party ID does not match your master customer ID |
| `MISSING_INVOICE_ADDRESS` | The `invoice_recipient` party carries no address |
| `INCOMPLETE_INVOICE_ADDRESS` | `name2`, `zip`, `city` or `countryCoded` is missing |
| `INVALID_INVOICE_ADDRESS` | The address does not match your invoice address in the JACOB customer master data — `name2`, `street`, `zip`, `city` and the resolved country code are compared |
| `INVALID_INVOICE_COUNTRY_CODE` | `countryCoded` is not a known ISO alpha-2 or alpha-3 code |

#### Delivery Address
| Code | Meaning |
| :--- | :--- |
| `MISSING_DELIVERY_RECIPIENT` | No party with the role `delivery` |
| `TOO_MANY_DELIVERY_RECIPIENTS` | More than one `delivery` party |
| `MISSING_DELIVERY_ADDRESS` | The `delivery` party carries no address |
| `TOO_MANY_DELIVERY_ADDRESSES` | The `delivery` party carries more than one address |
| `INCOMPLETE_DELIVERY_ADDRESS` | `name2`, `zip`, `city` or `countryCoded` is missing |
| `DELIVERY_ADDRESS_FIELD_TOO_SHORT` | One of these fields is below its [minimum length](orders/order_object.md#field-lengths) |
| `INVALID_DELIVERY_COUNTRY_CODE` | `countryCoded` is not a known ISO alpha-2 or alpha-3 code |

#### Items
| Code | Meaning |
| :--- | :--- |
| `MISSING_ITEMS` | The order carries no items |
| `MISSING_LINE_ITEM_ID` | `lineItemID` is not set |
| `DUPLICATE_LINE_ITEM_ID` | `lineItemID` is used by more than one item |
| `MISSING_PRODUCT_IDENTIFIER` | Neither `supplierPid` nor an `internationalPid` of type `gtin` is set |
| `INVALID_SKU` | `supplierPid` is not numeric |
| `SKU_TOO_SHORT` | `supplierPid` has fewer than 5 digits |
| `INVALID_GTIN` | The `gtin` `internationalPid` is not numeric or not exactly 13 characters long. Only checked when `supplierPid` is missing |
| `ARTICLE_NOT_ALLOWED` | The article is not orderable — internal process articles and 5-digit SKUs starting with `99` |
| `INVALID_QUANTITY` | The quantity is below 1 or not a whole number |
| `INVALID_PRICE` | `priceAmount` is not greater than 0 |
| `MISSING_LINE_AMOUNT` | `priceLineAmount` is not set |
| `INVALID_LINE_AMOUNT` | `priceLineAmount` is not `quantity × priceAmount` |
| `UNSUPPORTED_PRICE_SCALE` | A price or amount has more than 2 decimal places |

#### Summary and Field Lengths
| Code | Meaning |
| :--- | :--- |
| `TOTAL_AMOUNT_NOT_POSITIVE` | `totalAmount` is not greater than 0 |
| `INVALID_TOTAL_AMOUNT` | `totalAmount` is not the sum of all line amounts |
| `FIELD_TOO_LONG` | A field exceeds its [maximum length](orders/order_object.md#field-lengths); the message names the field |

### Sandbox-only Codes
These codes come from the [test article catalogue](sandbox.md#test-articles) rather than from the validation rules. They are returned synchronously as a `400` on `POST /orders`:

| Code | Trigger |
| :--- | :--- |
| `SKU_NOT_FOUND` | Test SKU `T-NOTFOUND` |
| `PRICE_MISMATCH` | Catalogue SKU `80000` |

The following codes apply only to the fields of the [webhook trigger request](sandbox.md#trigger-a-webhook-delivery):

| Code | Meaning |
| :--- | :--- |
| `MISSING_ORDER_ID` | `orderID` is missing or empty |
| `INVALID_ORDER_ID` | `orderID` is not in the format `JE` followed by digits |
| `MISSING_DOCUMENT_TYPE` | `documentType` is missing or empty |
| `INVALID_DOCUMENT_TYPE` | `documentType` is not `response`, `dispatch` or `invoice` |
