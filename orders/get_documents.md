## Get Order-related Documents
Order responses, dispatch notifications and invoices are fetched per order, by the JACOB order ID. [Look the order ID up](get_order.md) by your own order number first.

The three endpoints behave identically apart from the document they return.

### Request
| Method | URL | Document |
| :--- | :--- | :--- |
| GET | https://api.jacob.services/e-service/v1/orders/{orderID}/responses | Order responses (OpenTRANS `ORDERRESPONSE`) |
| GET | https://api.jacob.services/e-service/v1/orders/{orderID}/dispatches | Dispatch notifications (OpenTRANS `DISPATCHNOTIFICATION`) |
| GET | https://api.jacob.services/e-service/v1/orders/{orderID}/invoices | Invoices (OpenTRANS `INVOICE`) |

| Parameter | Description |
| :--- | :--- |
| `orderID` | The JACOB order ID, `JE` followed by digits, e.g. `JE912345671000` |

### Response
Each endpoint returns a JSON envelope holding a list of documents:

```json
{ "responses": [ { "orderResponseHeader": { "orderResponseInfo": { … } }, … } ] }
{ "dispatches": [ { "dispatchNotificationHeader": { … }, … } ] }
{ "invoices": [ { "invoiceHeader": { … }, … } ] }
```

An order may have more than one document of the same type, e.g. one invoice per partial delivery. The document structures follow the [OpenTRANS 2.1 specification](https://www.digital.iao.fraunhofer.de/de/publikationen/OpenTRANS21.html); their complete schemas are available in the [Swagger documentation](https://api.jacob.services/e-service/v1/docs/index.html).

| Status Code | Description |
| :--- | :--- |
| 200 | Request succeeded — the list may be empty |
| 400 | `orderID` is not in the format `JE` followed by digits |
| 401 | The API key is missing or invalid |
| 404 | No such order |
| 500 | Internal error |

**A document that does not exist yet is not an error.** As long as JACOB has not produced it, the endpoint answers `200` with an empty list or `null`. Keep polling — do not wait for a `404`.

### Polling
Documents become available as the order progresses: first the order response, then a dispatch notification per delivery, then the invoice. There is no push while you poll, so choose an interval that stays within the [rate limits](../README.md#rate-limits).

To avoid polling altogether, give the order a webhook URL and have each document delivered to your system instead — see [webhook delivery](../webhooks.md). Keep polling as a fallback even then.

### Example
```
curl "https://api.jacob.services/e-service/v1/orders/JE912345671000/responses" \
  -H "apikey: 123"
curl "https://api.jacob.services/e-service/v1/orders/JE912345671000/dispatches" \
  -H "apikey: 123"
curl "https://api.jacob.services/e-service/v1/orders/JE912345671000/invoices" \
  -H "apikey: 123"
```
