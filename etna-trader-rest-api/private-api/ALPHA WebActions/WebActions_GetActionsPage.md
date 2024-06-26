
<a name="webactions_getactionspage"></a>
#### Get web actions page
```
GET /v{version}/webactions
```


##### Description
Provides web actions Paged result


##### Parameters

|Type|Name|Description|Schema|Default|
|---|---|---|---|---|
|**Header**|**Authorization**  <br>*required*|This is the authorization token that you retrieved from the first endpoint (/token).|string||
|**Header**|**Et-App-Key**  <br>*required*|This is your app’s unique key that can be retrieved from the BO Companies widget in AutoShares.|string||
|**Path**|**version**  <br>*required*|This is the version of the API. Unless you have multiple versions of AutoShares’s API deployed in your environment, leave it at 1.0.|string|`"1"`|
|**Query**|**filter**  <br>*optional*|Filter query|string (String)||
|**Query**|**isDesc**  <br>*required*|Sorting direction. Desc if true, otherwise is asc|boolean||
|**Query**|**pageNumber**  <br>*required*|Page number|integer (int32)||
|**Query**|**pageSize**  <br>*required*|Page size|integer (int32)||
|**Query**|**sortBy**  <br>*required*|Sorting field|string||


##### Responses

|HTTP Code|Description|Schema|
|---|---|---|
|**200**|Actions paging result|[PagingResult[WebActionMapModel]](#pagingresult-webactionmapmodel)|
|**400**|Filter query is invalid or contains unsupported operations|No Content|
|**401**|The access level of the provided authorization token is not sufficient to perform this operation.|No Content|
|**403**|The provided Et-App-Key is incorrect.|No Content|
|**422**|A validation error occurred while processing the request.|No Content|
|**500**|Internal server error|No Content|


##### Produces

* `application/json`
* `text/json`



