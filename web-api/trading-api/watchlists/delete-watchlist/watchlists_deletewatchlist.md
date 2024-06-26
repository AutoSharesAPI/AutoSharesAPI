# Syntax

## Delete watchlist.

```
DELETE /v{version}/users/{userId}/watchlists/{watchlistId}
```

### Description

This API endpoint enables you to delete an existing watchlist.

### Parameters

| Type       | Name                                                       | Description                                                                                                                          | Schema          | Default |
| ---------- | ---------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------ | --------------- | ------- |
| **Header** | <p><strong>Authorization</strong><br><em>required</em></p> | This is the authorization token that you retrieved from the first endpoint (/token).                                                 | string          |         |
| **Path**   | <p><strong>userId</strong><br><em>required</em></p>        | This is the internal identifier of the user whose watchlist needs to be deleted.                                                     | integer (int32) |         |
| **Path**   | <p><strong>version</strong><br><em>required</em></p>       | This is the version of the API. Unless you have multiple versions of AutoShares’s API deployed in your environment, leave it at 1.0. | string          | `"1"`   |
| **Path**   | <p><strong>watchlistId</strong><br><em>required</em></p>   | This is the internal identifier of the watchlist that needs to be deleted.                                                           | integer (int32) |         |

### Responses

| HTTP Code | Description                                                                                       | Schema     |
| --------- | ------------------------------------------------------------------------------------------------- | ---------- |
| **200**   | OK                                                                                                | object     |
| **204**   | The watchlist was successfully deleted                                                            | No Content |
| **401**   | The access level of the provided authorization token is not sufficient to perform this operation. | No Content |
| **403**   | The provided Et-App-Key is incorrect.                                                             | No Content |
| **409**   | The watchlist couldn’t be deleted due to some conflict                                            | No Content |
| **422**   | A validation error occurred while processing the request.                                         | No Content |
| **500**   | Internal server error                                                                             | No Content |

### Produces

* `application/json`
* `text/json`
