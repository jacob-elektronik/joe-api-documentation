## Webhook Delivery
Instead of [polling for documents](orders/get_documents.md), you can have JOE POST each document to an HTTPS endpoint of your choice as soon as it becomes available.

Webhook delivery is optional and enabled per order. There is no subscription API and no default URL stored on your account.

### Setup
Set the target URL in the order's header UDX field `UDX.WEBHOOK` — `orderHeader.orderInfo.headerUDX` in JSON, `HEADER_UDX` in XML:

```json
{
  "orderHeader": {
    "orderInfo": {
      "headerUDX": {
        "UDX.WEBHOOK": "https://your-server.example.com/jacob-webhook"
      }
    }
  }
}
```

```xml
<HEADER_UDX>
  <UDX.WEBHOOK>https://your-server.example.com/jacob-webhook</UDX.WEBHOOK>
</HEADER_UDX>
```

The field is optional: an order without it is accepted normally, it just receives no delivery. Only `https` URLs are accepted — an order carrying an invalid URL is rejected with the error code `INVALID_WEBHOOK_URL`.

### Payload
What is delivered is the document itself — the same structure the [document endpoints](orders/get_documents.md) return. There is no event envelope, no event type and no additional metadata.

The `Content-Type` of the delivery matches the format you submitted the order in, `application/json` or `application/xml`.

Order responses, dispatch notifications and invoices are delivered. Credit memos are not.

### Responding to a Delivery
Any `2xx` response counts as delivered successfully.

A delivery is retried on `408`, `429` and every `5xx` response, as well as on timeouts and connection errors. **Any other `4xx` response is treated as final** — the document is then not delivered again.

### Retries
After a failed first attempt, up to six retries follow:

| Retry | Delay after the previous attempt |
| :--- | :--- |
| 1 | 10 minutes |
| 2 | 30 minutes |
| 3 | 1 hour |
| 4 | 4 hours |
| 5 | 12 hours |
| 6 | 24 hours |

That is up to seven delivery attempts over roughly 42 hours. After that the delivery is dropped; there is no queue it is re-sent from later. The documents themselves remain available via the [document endpoints](orders/get_documents.md) — **keep polling as a fallback.**

**Expect duplicate deliveries.** If your endpoint answers too slowly or with an error although it has already processed the document, the same document is delivered again. Process documents idempotently.

### Signature
Deliveries carry no signature header. Use a URL that cannot be guessed, and reconcile against the [document endpoints](orders/get_documents.md) where you need certainty.

### Testing Webhooks
In the sandbox, deliveries are not triggered by document processing but by you — see [sandbox](sandbox.md#trigger-a-webhook-delivery). Note that the sandbox makes exactly one delivery attempt; the retry chain above applies to production only.
