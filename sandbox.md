## Sandbox
The sandbox is a permanently available test environment — also after go-live, for regression tests. It runs the same code as production, so its behaviour is identical apart from the specifics below.

`https://api.jacob.services/sandbox-e-service/v1/`

Use the sandbox API key with the sandbox base URL. Sandbox orders are kept in memory, are visible only to you, and expire automatically after at most 48 hours.

### Differences to Production
* **Documents are synthesized from the stored order.** After a successful `POST`, `/responses`, `/dispatches` and `/invoices` immediately return exactly one document each. The sandbox therefore does not reproduce the timing of the real document chain — in production documents appear only once JACOB has produced them. Do not test your polling intervals against sandbox timings.
* **Webhook deliveries are triggered by you**, not by document processing, and there is exactly one delivery attempt. A failed delivery is logged and dropped; the [retry chain](webhooks.md#retries) applies to production only.
* **Article validation runs against the fixed test catalogue** below instead of the JACOB assortment.
* **The `/test/*` endpoints exist only in the sandbox.** In production they are not registered and answer with a `404`, even though the Swagger documentation currently lists them for both environments.

Everything else — the validation rules, the [error codes](errors.md) and the response formats — is the same as in production.

### Test Endpoints
| Method | URL | Description |
| :--- | :--- | :--- |
| GET | https://api.jacob.services/sandbox-e-service/v1/test/skus | List the test articles |
| POST | https://api.jacob.services/sandbox-e-service/v1/test/trigger | Trigger a webhook delivery |
| DELETE | https://api.jacob.services/sandbox-e-service/v1/test/reset | Delete all your sandbox orders |

### Test Articles
`GET /test/skus` returns the catalogue. Ordering one of the error SKUs triggers its code deterministically, which lets you exercise your error handling without constructing invalid orders:

| SKU | Price | Behaviour |
| :--- | :--- | :--- |
| `10000` | 10.00 | Happy path, single item |
| `10001` | 25.00 | Happy path, multiple quantity |
| `80000` | 15.00 | Triggers `PRICE_MISMATCH` |
| `80001` | 20.00 | Triggers `INVALID_INVOICE_ADDRESS` |
| `80002` | 20.00 | Triggers `INCOMPLETE_DELIVERY_ADDRESS` |
| `T-NOTFOUND` | — | Triggers `SKU_NOT_FOUND` |

The error SKUs trigger their code from the catalogue entry itself, whatever price and quantity you send — no price comparison takes place. SKUs that are not in the catalogue are accepted in the sandbox as long as they pass the [normal item validation](orders/place_order.md#validation), so you can also test with your own article numbers.

The catalogue check runs before the other validation rules, so an order carrying an error SKU returns that code alone; remaining violations of the same order only surface once the error SKU is gone.

### Trigger a Webhook Delivery
`POST https://api.jacob.services/sandbox-e-service/v1/test/trigger`

Delivers the document synthesized from the order to the order's `UDX.WEBHOOK` URL, in the format the order was submitted in.

| Field | Description |
| :--- | :--- |
| `orderID` | The JACOB order ID of the sandbox order, `JE` followed by digits |
| `documentType` | `response`, `dispatch` or `invoice` |

```
curl -X POST https://api.jacob.services/sandbox-e-service/v1/test/trigger \
  -H "apikey: 123" \
  -H "Content-Type: application/json" \
  -d '{ "orderID": "JE912345671000", "documentType": "response" }'

HTTP/1.1 202 Accepted
```

| Status Code | Description |
| :--- | :--- |
| 202 | The delivery was triggered |
| 400 | The request is invalid — see the [trigger error codes](errors.md#sandbox-only-codes) |
| 404 | Unknown order ID, or the order belongs to another customer |

If the order carries no webhook URL, the call is still accepted with a `202` and nothing is delivered.

### Reset the Sandbox
`DELETE https://api.jacob.services/sandbox-e-service/v1/test/reset`

Deletes all your sandbox orders and answers with `204 No Content`. Sandbox orders expire on their own after at most 48 hours, so a reset is only needed to re-use an order number sooner.

```
curl -X DELETE https://api.jacob.services/sandbox-e-service/v1/test/reset \
  -H "apikey: 123"
```

### Recommended Test Scenarios
We recommend running these scenarios before you go live. Support requests can be handled much faster if these tests passed on your side.

| # | Test case | How | Expected result |
| :--- | :--- | :--- | :--- |
| T-01 | Happy path | SKU `10000`, quantity 1, `priceAmount` 10.00 | `201 Created` without a body → resolve the order ID via `GET /orders?customerOrderID={id}` → `/responses`, `/dispatches` and `/invoices` each return one document |
| T-02 | Unknown SKU | Order SKU `T-NOTFOUND` | `400`, `details` holds `SKU_NOT_FOUND` — immediately, not via polling |
| T-03 | Price mismatch | Order catalogue SKU `80000` | `400`, `details` holds `PRICE_MISMATCH` |
| T-04 | Duplicate order number | Send the same `orderInfo.orderID` twice | 2nd request: `400`, `details` holds `DUPLICATE_ORDER`. An order that was rejected earlier may be sent again under the same ID |
| T-05 | Incomplete delivery address | Order catalogue SKU `80002` — or send an order whose delivery address is missing `name2`, `zip`, `city` or `countryCoded` | `400`, `details` holds `INCOMPLETE_DELIVERY_ADDRESS` |
| T-06 | Rate limit | Send more requests than the [rate limit](README.md#rate-limits) allows | `429`. The response comes from the API gateway, not from JOE, and carries no JOE error code |
| T-07 | Deviating invoice address | Order catalogue SKU `80001` | `400`, `details` holds `INVALID_INVOICE_ADDRESS` |
| T-08 | Several violations at once | Send an order with two errors, e.g. a missing `currency` and a 4-digit SKU | `400` with several entries in `details`. Verify that your client evaluates all of them, not just the first |
| T-09 | Webhook delivery | Place an order carrying `UDX.WEBHOOK`, then `POST /test/trigger` with `documentType: response` | `202 Accepted`; the document arrives at your webhook URL — without a signature header, in the format of the order. The sandbox makes a single delivery attempt |
| T-10 | Order by GTIN | Item without `supplierPid`, instead an `internationalPid` of type `gtin` with 13 digits | `201 Created`. With 12 or 14 digits: `400`, `details` holds `INVALID_GTIN` |
