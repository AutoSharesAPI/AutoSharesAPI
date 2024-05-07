# Syntax

## Delete price alert

```
DELETE /v{version}/users/{userId}/pricealerts/{alertId}
```

### Description

This API endpoint enables you to delete an existing price alert.

### Parameters

| Type       | Name                                                       | Description                                                                                                                          | Schema          | Default |
| ---------- | ---------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------ | --------------- | ------- |
| **Header** | <p><strong>Authorization</strong><br><em>required</em></p> | This is the authorization token that you retrieved from the first endpoint (/token).                                                 | string          |         |
| **Path**   | <p><strong>alertId</strong><br><em>required</em></p>       | This is the internal identifier of the price alert that must be deleted.                                                             | integer (int32) |         |
| **Path**   | <p><strong>userId</strong><br><em>required</em></p>        | This is the internal identifier of the user whose price alert must be deleted.                                                       | integer (int32) |         |
| **Path**   | <p><strong>version</strong><br><em>required</em></p>       | This is the version of the API. Unless you have multiple versions of AutoShares’s API deployed in your environment, leave it at 1.0. | string          | `"1"`   |

### Responses

| HTTP Code | Description                                                                                       | Schema     |
| --------- | ------------------------------------------------------------------------------------------------- | ---------- |
| **200**   | OK                                                                                                | object     |
| **204**   | Successful request, the price alert has been successfully deleted.                                | No Content |
| **401**   | The access level of the provided authorization token is not sufficient to perform this operation. | No Content |
| **409**   | Conflict                                                                                          | No Content |
| **422**   | A validation error occurred while processing the request.                                         | No Content |
| **500**   | Internal server error                                                                             | No Content |

### Produces

* `application/json`
* `text/json`
