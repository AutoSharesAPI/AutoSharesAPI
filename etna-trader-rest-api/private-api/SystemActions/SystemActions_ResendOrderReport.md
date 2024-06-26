
<a name="systemactions_resendorderreport"></a>
#### Resend order execution repost
```
PUT /v{version}/systemactions/orders/resendorderreports
```


##### Description
Resend order execution reports to Oms


##### Parameters

|Type|Name|Description|Schema|Default|
|---|---|---|---|---|
|**Header**|**Authorization**  <br>*required*|This is the authorization token that you retrieved from the first endpoint (/token).|string||
|**Header**|**Et-App-Key**  <br>*required*|This is your app’s unique key that can be retrieved from the BO Companies widget in AutoShares.|string||
|**Path**|**version**  <br>*required*|This is the version of the API. Unless you have multiple versions of AutoShares’s API deployed in your environment, leave it at 1.0.|string|`"1"`|
|**Body**|**body**  <br>*required*|Order report request parameters|[ResendOrderReportRequest](#resendorderreportrequest)||


##### Responses

|HTTP Code|Description|Schema|
|---|---|---|
|**200**|Action were successfully executed|[ResendOrderReportRequest](#resendorderreportrequest)|
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



