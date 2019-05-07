
<a name="securities_getoptionsexpirations"></a>
#### Get options expirations set
```
GET /v{version}/options/expirations
```


##### Description
Get options expirations by underlying asset symbol


##### Parameters

|Type|Name|Description|Schema|Default|
|---|---|---|---|---|
|**Header**|**Authorization**  <br>*required*|Bearer type token string|string||
|**Header**|**Et-App-Key**  <br>*required*|Application key|string||
|**Path**|**version**  <br>*required*|The requested API version|string|`"1"`|
|**Query**|**currency**  <br>*optional*|Target currency, optional|string||
|**Query**|**exchange**  <br>*optional*|Target exchange, optional|string||
|**Query**|**underlying**  <br>*required*|Underlying asset symbol|string||


##### Responses

|HTTP Code|Description|Schema|
|---|---|---|
|**200**|Expirations dates|< [OptionExpirationResource](#optionexpirationresource) > array|
|**401**|Authorization has been denied for this request.|No Content|
|**403**|Application key is not defined or does not exist|No Content|
|**422**|Validation error occurred while processing entity|No Content|
|**500**|Internal server error|No Content|


##### Produces

* `application/json`
* `text/json`


