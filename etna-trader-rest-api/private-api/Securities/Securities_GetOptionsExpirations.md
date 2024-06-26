
<a name="securities_getoptionsexpirations"></a>
#### Get options expirations set
```
GET /v{version}/options/expirations
```


##### Description
This API endpoint enables you to retrieve expiration dates of options with a specific underlying security.


##### Parameters

|Type|Name|Description|Schema|Default|
|---|---|---|---|---|
|**Header**|**Authorization**  <br>*required*|This is the authorization token that you retrieved from the first endpoint (/token).|string||
|**Header**|**Et-App-Key**  <br>*required*|This is your app’s unique key that can be retrieved from the BO Companies widget in AutoShares.|string||
|**Path**|**version**  <br>*required*|This is the version of the API. Unless you have multiple versions of AutoShares’s API deployed in your environment, leave it at 1.0.|string|`"1"`|
|**Query**|**currency**  <br>*optional*|This is the exchange on which the options are listed (use it if you have multiple options with the same ticker but listed on different exchanges).|string||
|**Query**|**exchange**  <br>*optional*|This is the currency in which the options are denominated (use it if you have multiple options with the same ticker but denominated in different currencies).|string||
|**Query**|**underlying**  <br>*required*|This is the ticker symbol of the underlying security of the options whose expiration dates need to be retrieved.|string||


##### Responses

|HTTP Code|Description|Schema|
|---|---|---|
|**200**|Successful request, JSON data is returned, containing the expiration dates of options with the specified underlying security.|< [OptionExpirationResource](#optionexpirationresource) > array|
|**401**|The access level of the provided authorization token is not sufficient to perform this operation.|No Content|
|**403**|The provided Et-App-Key is incorrect.|No Content|
|**422**|A validation error occurred while processing the request.|No Content|
|**500**|Internal server error|No Content|


##### Produces

* `application/json`
* `text/json`



