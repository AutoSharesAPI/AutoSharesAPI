
<a name="useraccounts_getuseraccounts"></a>
#### Get user accounts
```
GET /v{version}/users/{userId}/accounts
```


##### Description
This API endpoint returns the list of trading accounts bound to a particular user.


##### Parameters

|Type|Name|Description|Schema|Default|
|---|---|---|---|---|
|**Header**|**Authorization**  <br>*required*|This is the authorization token that you retrieved from the first endpoint (/token).|string||
|**Header**|**Et-App-Key**  <br>*required*|This is your app’s unique key that can be retrieved from the BO Companies widget in AutoShares.|string||
|**Path**|**userId**  <br>*required*|This is the unique identifier of the user in AutoShares.|integer (int32)||
|**Path**|**version**  <br>*required*|This is the version of the API. Unless you have multiple versions of AutoShares’s API deployed in your environment, leave it at 1.0.|string|`"1"`|


##### Responses

|HTTP Code|Description|Schema|
|---|---|---|
|**200**|Successful request, returns the list of trading accounts bound to the user whose ID was specified in the request path.|< [UserAccountModel](#useraccountmodel) > array|
|**401**|The access level of the provided authorization token is not sufficient to perform this operation.|No Content|
|**403**|The provided Et-App-Key is incorrect.|No Content|
|**422**|A validation error occurred while processing the request.|No Content|
|**500**|Internal server error|No Content|


##### Produces

* `application/json`
* `text/json`



