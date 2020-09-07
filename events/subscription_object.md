## Subscription Object

### Request Example
```json
{
  "createdAt": "2020-09-01T12:17:02",
  "creator": "Max Mustermann",
  "event": "invoice.generated",
  "identifier": {
    "type": "CustomerId",
    "value": "112233"
  },
  "webhook": {
    "url": "https://example.com/webhook"
  }
}
```

The following `event`s are currently supported:
* `response.generated`
* `invoice.generated`
* `dispatch.generated`

### Response Example
The response object is the request object with an additional `subscriptionId` field.
```json
{
  "createdAt": "2020-09-01T12:17:02",
  "creator": "Max Mustermann",
  "event": "invoice.generated",
  "identifier": {
    "type": "CustomerId",
    "value": "112233"
  },
  "webhook": {
    "url": "https://example.com/webhook"
  },
  "subscriptionId": "d8bbd7e0-f0df-11ea-adc1-0242ac120002"
}
```

#### Authentication
The `webhook` object accepts an optional `authentication` object to allow for access restricted callback endpoints. Three types of authentication/authorization are supported.

* Basic HTTP Authentication:
    ```json
        ...
      },
      "webhook": {
        "url": "https://example.com/webhook",
        "authentication": {
          "type": "basic",
          "user": "jacob_callback",
          "password": "3858f62230ac3c915f300c664312c63f"
        }
      }
    }
    ```
  
* Authorization via custom HTTP header, e.g. `x-access-token: 3858f62230ac3c915f300c664312c63f`:
    ```json
        ...
      },
      "webhook": {
        "url": "https://example.com/webhook",
        "authentication": {
          "type": "header",
          "header": "x-access-token",
          "key": "3858f62230ac3c915f300c664312c63f"
        }
      }
    }
    ```
  
* Authorization via query parameter, e.g. `http://example.com/webhook?access_token=3858f62230ac3c915f300c664312c63f`:
    ```json
        ...
      },
      "webhook": {
        "url": "https://example.com/webhook",
        "authentication": {
          "type": "query",
          "queryParam": "access_token",
          "key": "3858f62230ac3c915f300c664312c63f"
        }
      }
    }
    ```

