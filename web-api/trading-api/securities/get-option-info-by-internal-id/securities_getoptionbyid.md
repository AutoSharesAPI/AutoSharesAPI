# Syntax

## Get option by id

```
GET /v{version}/options/{id}
```

### Description

This API endpoint enables you to retrieve detailed information about a specific option by providing its internal identifier in AutoShares.

### Parameters

| Type       | Name                                                       | Description                                                                                                                          | Schema          | Default |
| ---------- | ---------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------ | --------------- | ------- |
| **Header** | <p><strong>Authorization</strong><br><em>required</em></p> | This is the authorization token that you retrieved from the first endpoint (/token).                                                 | string          |         |
| **Path**   | <p><strong>id</strong><br><em>required</em></p>            | This is the internal identifier of the enquired option in AutoShares.                                                                | integer (int32) |         |
| **Path**   | <p><strong>version</strong><br><em>required</em></p>       | This is the version of the API. Unless you have multiple versions of AutoShares’s API deployed in your environment, leave it at 1.0. | string          | `"1"`   |

### Responses

| HTTP Code | Description                                                                                          | Schema                                                        |
| --------- | ---------------------------------------------------------------------------------------------------- | ------------------------------------------------------------- |
| **200**   | Successful request, JSON data containing detailed information about the enquired option is returned. | [OptionResource](securities\_getoptionbyid.md#optionresource) |
| **401**   | The access level of the provided authorization token is not sufficient to perform this operation.    | No Content                                                    |
| **404**   | Enquired option is non-existent in AutoShares.                                                       | No Content                                                    |
| **422**   | A validation error occurred while processing the request.                                            | No Content                                                    |
| **500**   | Internal server error                                                                                | No Content                                                    |

### Produces

* `application/json`
* `text/json`
