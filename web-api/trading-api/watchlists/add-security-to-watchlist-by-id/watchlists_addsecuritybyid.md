# Syntax

## Add security by Id.

```
PUT /v{version}/users/{userId}/watchlists/{watchlistId}/securities/{securityId}
```

### Description

This API endpoint enables you add a security to a custom watchlist by providing the security’s internal identifier in the request header.

### Parameters

| Type       | Name                                                       | Description                                                                                                                          | Schema          | Default |
| ---------- | ---------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------ | --------------- | ------- |
| **Header** | <p><strong>Authorization</strong><br><em>required</em></p> | This is the authorization token that you retrieved from the first endpoint (/token).                                                 | string          |         |
| **Path**   | <p><strong>securityId</strong><br><em>required</em></p>    | This is the internal identifier of the security that needs to be added to the specified watchlist.                                   | integer (int32) |         |
| **Path**   | <p><strong>userId</strong><br><em>required</em></p>        | This is the internal identifier of the user whose watchlist needs to be modified.                                                    | integer (int32) |         |
| **Path**   | <p><strong>version</strong><br><em>required</em></p>       | This is the version of the API. Unless you have multiple versions of AutoShares’s API deployed in your environment, leave it at 1.0. | string          | `"1"`   |
| **Path**   | <p><strong>watchlistId</strong><br><em>required</em></p>   | This is the internal identifier of the watchlist that needs to be appended by a new security.                                        | integer (int32) |         |

### Responses

| HTTP Code | Description                                                                                       | Schema                                                          |
| --------- | ------------------------------------------------------------------------------------------------- | --------------------------------------------------------------- |
| **200**   | Successful request, JSON data containing the modified watchlist is returned.                      | [WatchlistModel](watchlists\_addsecuritybyid.md#watchlistmodel) |
| **401**   | The access level of the provided authorization token is not sufficient to perform this operation. | No Content                                                      |
| **409**   | The watchlist couldn’t be modified due to some conflict (perhaps the watchlist is read-only       | No Content                                                      |
| **422**   | A validation error occurred while processing the request.                                         | No Content                                                      |
| **500**   | Internal server error                                                                             | No Content                                                      |

### Produces

* `application/json`
* `text/json`
