
# JOE API Documentation

JOE stands for [JACOB](https://www.jacob.de/) Order Engine and describes a standardized interface to handle orders. The JOE API allows placing orders, retrieving order-related documents like invoices, and subscribing to order-related events. The main goal of JOE is to avoid long integration phases by keeping things simple.

Feel free to [contact us](mailto:joe.api@jacob.de) with any issues regarding this API.

## Authentication
Using the JOE API requires an API key which must be appended to each request as a query parameter:
```
https://api.jacob.services/1.0/joe?apikey=123
```

**Note that API keys are customer-specific and should be kept confidential.**

## Orders

All documents, i.e. orders, order responses, invoices and dispatch notifications, are represented as JSON or XML. The XML representations loosely follow the [OpenTRANS 2.1 specification](https://www.digital.iao.fraunhofer.de/de/publikationen/OpenTRANS21.html), the corresponding JSON ones are equivalent. There are [examples for both formats](orders/document_objects.md).

The default input and output format for documents is XML. This can be changed to JSON by setting the request's `Content-Type` or `Accept` header to `application/json`.

### Placing Orders
| Method | URL | Description | Details |
| :--- | :--- | :--- | :--- |
| POST | https://api.jacob.services/1.0/joe/{orderId} | Place an order | [Link](orders/place_order.md) |

### Order Information
| Method | URL | Description | Details |
| :--- | :--- | :--- | :--- |
| GET | https://api.jacob.services/1.0/joe | List all orders | [Link](orders/list_orders.md) |
| GET | https://api.jacob.services/1.0/joe/{orderId} | Get document status | [Link](orders/get_document_status.md) |

### Order-related Documents
| Method | URL | Description | Details |
| :--- | :--- | :--- | :--- |
| GET | https://api.jacob.services/1.0/joe/{orderId}/order | Download an order | [Link](orders/get_order.md) |
| GET | https://api.jacob.services/1.0/joe/{orderId}/response | Download an order response | [Link](orders/get_response.md) |
| GET | https://api.jacob.services/1.0/joe/{orderId}/invoice | Download an invoice | [Link](orders/get_invoice.md) |
| GET | https://api.jacob.services/1.0/joe/{orderId}/dispatch | Download a dispatch notification | [Link](orders/get_dispatch.md) |

## Events
JOE generates events whenever new order response, invoice or dispatch notification documents become available. The event subscription mechanism allows getting notified about such events.

### Technical Details
Getting notified requires an HTTP endpoint. Subscribing means specifying the desired event type and the HTTP endpoint. Once subscribed, every time an event of the desired type occurs JOE will POST the JSON representation of the event to the user's endpoint.

Endpoints may be access restricted by one of the following mechanisms:
* ['Basic' HTTP Authentication](https://en.wikipedia.org/wiki/Basic_access_authentication)
* Authorization via custom HTTP header, e.g. `x-access-token: 3858f622`
* Authorization via query parameter, e.g. `http://example.com/webhook?token=3858f622`

See the description of the [subscription object](events/subscription_object.md) for details.

### Subscribing and Unsubscribing
| Method | URL | Description | Details |
| :--- | :--- | :--- | :--- |
| POST | https://api.jacob.services/1.0/joe/events/subscriptions | Subscribe to an event | [Link](events/subscribe.md) |
| DELETE | https://api.jacob.services/1.0/joe/events/subscriptions/{subId} | Unsubscribe from an event | [Link](events/unsubscribe.md) |

### Managing Subscriptions
| Method | URL | Description | Details |
| :--- | :--- | :--- | :--- |
| GET | https://api.jacob.services/1.0/joe/events/subscriptions/{subId} | Fetch a subscription | [Link](events/get_subscription.md) |
| PATCH | https://api.jacob.services/1.0/joe/events/subscriptions/{subId} | Change a subscription | [Link](events/change_subscription.md) |
| PUT | https://api.jacob.services/1.0/joe/events/subscriptions/{subId} | Replace a subscription | [Link](events/replace_subscription.md) |
