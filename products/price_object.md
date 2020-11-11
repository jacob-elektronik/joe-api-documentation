## Price Information Object

This object provides general price and stock information.

### Example
```json
{
  "sku": 6252355,
  "net": 10.4,
  "qty": 20,
  "currency": "EUR"
}
```

### Description

| Key | Value Description |
| --- | --- |
| sku | Product SKU |
| net | The product's net price |
| qty | Amount of items currently in stock |
| currency | Currency of the net price |

### Caveats
The net price is provided as a floating-point number and might have excess decimal places, like `123.456789`.