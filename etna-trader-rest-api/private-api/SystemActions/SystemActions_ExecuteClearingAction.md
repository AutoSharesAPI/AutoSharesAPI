
<a name="systemactions_executeclearingaction"></a>
#### Executes specified system action
```
PUT /v{version}/systemactions/clearing
```


##### Description
System actions list result


##### Parameters

|Type|Name|Description|Schema|Default|
|---|---|---|---|---|
|**Header**|**Authorization**  <br>*required*|This is the authorization token that you retrieved from the first endpoint (/token).|string||
|**Header**|**Et-App-Key**  <br>*required*|This is your app’s unique key that can be retrieved from the BO Companies widget in AutoShares.|string||
|**Path**|**version**  <br>*required*|This is the version of the API. Unless you have multiple versions of AutoShares’s API deployed in your environment, leave it at 1.0.|string|`"1"`|
|**Body**|**body**  <br>*required*|List with handlers to be executed|[ClearingAction](#clearingaction)||


##### Responses

|HTTP Code|Description|Schema|
|---|---|---|
|**200**|Action were successfully executed|[ClearingAction](#clearingaction)|
|**401**|The access level of the provided authorization token is not sufficient to perform this operation.|No Content|
|**403**|The provided Et-App-Key is incorrect.|No Content|
|**409**|An error occurred while executing the action|No Content|
|**422**|A validation error occurred while processing the request.|No Content|
|**500**|Internal server error|No Content|


##### Consumes

* `application/json`
* `text/json`


##### Produces

* `application/json`
* `text/json`



