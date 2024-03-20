# Syntax

## Get order

```
GET /v{version}/accounts/{accountId}/orders/{orderId}
```

### Description

This API endpoint enables you to retrieve information about a particular order

### Parameters

| Type       | Name                                                       | Description                                                                                                                          | Schema          | Default |
| ---------- | ---------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------ | --------------- | ------- |
| **Header** | <p><strong>Authorization</strong><br><em>required</em></p> | This is the authorization token that you retrieved from the first endpoint (/token).                                                 | string          |         |
| **Path**   | <p><strong>accountId</strong><br><em>required</em></p>     | This is the unique identifier of the trading account whose order’s information needs to be retrieved.                                | integer (int32) |         |
| **Path**   | <p><strong>orderId</strong><br><em>required</em></p>       | This is the ID of the order whose information needs to be retrieved.                                                                 | integer (int32) |         |
| **Path**   | <p><strong>version</strong><br><em>required</em></p>       | This is the version of the API. Unless you have multiple versions of AutoShares’s API deployed in your environment, leave it at 1.0. | string          | `"1"`   |

### Responses

| HTTP Code | Description                                                                                       | Schema                                             |
| --------- | ------------------------------------------------------------------------------------------------- | -------------------------------------------------- |
| **200**   | Successful request, a JSON with the order’s detailed information is returned.                     | [OrderResource](orders\_getorder.md#orderresource) |
| **401**   | The access level of the provided authorization token is not sufficient to perform this operation. | No Content                                         |
| **403**   | The provided Et-App-Key is incorrect.                                                             | No Content                                         |
| **422**   | A validation error occurred while processing the request.                                         | No Content                                         |
| **500**   | Internal server error                                                                             | No Content                                         |

### Produces

* `application/json`
* `text/json`
