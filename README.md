# JOE API Documentation

JOE stands for [JACOB](https://www.jacob.de/) Order Engine and describes a standardized interface to handle orders. The JOE API allows placing orders and retrieving order-related documents like order responses, dispatch notifications and invoices. The main goal of JOE is to avoid long integration phases by keeping things simple.

This documentation describes **JOE 2.0**, the current version of the API.

Feel free to [contact us](mailto:edi@jacob.de) with any issues regarding this API.

## Getting Started
Send an email to [edi@jacob.de](mailto:edi@jacob.de) with your customer number, a technical contact and your preferred document format (JSON or XML). You will receive two API keys — one for the sandbox, one for production — within a few working days. Build and test your integration against the [sandbox](sandbox.md), then switch to the production base URL to go live.

## Base URLs
| Environment | Base URL |
| :--- | :--- |
| Production | https://api.jacob.services/e-service/v1/ |
| Sandbox | https://api.jacob.services/sandbox-e-service/v1/ |

All paths in this documentation are relative to one of these base URLs. Both environments run the same code, so their behaviour is identical apart from the [sandbox specifics](sandbox.md).

## Authentication
Using the JOE API requires an API key which must be sent as an HTTP header with each request:
```
apikey: 123
```

**Keep in mind that API keys are customer-specific and should be kept confidential.**

The API key is not accepted as a query parameter. All requests must use TLS 1.2 or higher.

## Formats
All documents, i.e. orders, order responses, invoices and dispatch notifications, are represented as JSON or XML. The XML representations loosely follow the [OpenTRANS 2.1 specification](https://www.digital.iao.fraunhofer.de/de/publikationen/OpenTRANS21.html), the corresponding JSON ones are equivalent. See the [order object](orders/order_object.md) for examples of both formats.

The format of an order is chosen per request by setting the `Content-Type` header to `application/json`, `application/xml` or `text/xml`. An unspecified or unknown `Content-Type` is treated as JSON. API responses are always JSON.

## Rate Limits
100 requests per minute and 1,000 requests per hour. Exceeding the limit yields an HTTP `429` from the API gateway, without a JOE error code.

## Orders

### Placing Orders
| Method | URL | Description | Details |
| :--- | :--- | :--- | :--- |
| POST | https://api.jacob.services/e-service/v1/orders | Place an order | [Link](orders/place_order.md) |

### Order Information
| Method | URL | Description | Details |
| :--- | :--- | :--- | :--- |
| GET | https://api.jacob.services/e-service/v1/orders?customerOrderID={id} | Look up an order by your own order number | [Link](orders/get_order.md) |
| GET | https://api.jacob.services/e-service/v1/orders/{orderID} | Download an order | [Link](orders/get_order.md) |

### Order-related Documents
| Method | URL | Description | Details |
| :--- | :--- | :--- | :--- |
| GET | https://api.jacob.services/e-service/v1/orders/{orderID}/responses | Download the order responses | [Link](orders/get_documents.md) |
| GET | https://api.jacob.services/e-service/v1/orders/{orderID}/dispatches | Download the dispatch notifications | [Link](orders/get_documents.md) |
| GET | https://api.jacob.services/e-service/v1/orders/{orderID}/invoices | Download the invoices | [Link](orders/get_documents.md) |

`{orderID}` is the JACOB order ID in the format `JE` followed by digits, e.g. `JE912345671000`. It is assigned by JACOB and [looked up via your own order number](orders/get_order.md) — placing an order does not return it.

## Webhook Delivery
JOE generates an order response, dispatch notification or invoice whenever such a document becomes available. Instead of polling the document endpoints, you can have JOE POST each document to an HTTPS endpoint of your choice. The target URL is set per order, so no subscription management is required.

See [webhook delivery](webhooks.md) for the setup, the payload, the retry behaviour and its limits.

The alternative to webhook delivery is polling, i.e. [fetching the documents](orders/get_documents.md) at regular intervals. Keep polling as a fallback even when you use webhooks.

## Errors
Validation errors are reported synchronously as an HTTP `400` listing every violation of the request. See [errors](errors.md) for the response format and the complete list of error codes.

## Sandbox
The sandbox is a permanently available test environment with its own API key, a fixed catalogue of test articles and endpoints to reset the store and to trigger webhook deliveries. See [sandbox](sandbox.md), including the test scenarios we recommend running before you go live.

## Migrating from JOE v1
| Aspect | JOE v1 | JOE 2.0 |
| :--- | :--- | :--- |
| Base URL | `https://api.jacob.services/1.0/joe` | `https://api.jacob.services/e-service/v1/` |
| Authentication | `?apikey=` query parameter | `apikey` HTTP header |
| Order ID | your own `ORDER_ID`, echoed in the `Location` header | JACOB-assigned `JE…` ID, [looked up by your order number](orders/get_order.md); the POST returns no body |
| Validated parties | `buyer` and `supplier` | `invoice_recipient` and `delivery` |
| Duplicate order number | HTTP `409` | HTTP `400` with error code `DUPLICATE_ORDER` |
| Document retrieval | polling or event subscriptions | polling or [per-order webhook URL](webhooks.md) |
| Event subscriptions | `/events/subscriptions` endpoints | removed, replaced by the per-order webhook URL |

## Reference
* Swagger documentation: [api.jacob.services/e-service/v1/docs/index.html](https://api.jacob.services/e-service/v1/docs/index.html) (public, no authentication required)
* Contact: [edi@jacob.de](mailto:edi@jacob.de)
