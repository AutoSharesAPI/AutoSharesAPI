
<a name="orders_placeorder"></a>
#### Place order
```
POST /v{version}/accounts/{accountId}/orders
```


##### Description
This API endpoint enables you to place a new order in AutoShares.


##### Parameters

|Type|Name|Description|Schema|Default|
|---|---|---|---|---|
|**Header**|**Authorization**  <br>*required*|This is the authorization token that you retrieved from the first endpoint (/token).|string||
|**Header**|**Et-App-Key**  <br>*required*|This is your app’s unique key that can be retrieved from the BO Companies widget in AutoShares.|string||
|**Path**|**accountId**  <br>*required*|This is the unique identifier of the trading account on which a new order is to be verified.|integer (int32)||
|**Path**|**version**  <br>*required*|This is the version of the API. Unless you have multiple versions of AutoShares’s API deployed in your environment, leave it at 1.0.|string|`"1"`|
|**Query**|**currency**  <br>*optional*|This is the currency in which the underlying security of the order is denominated.|string||
|**Query**|**exchange**  <br>*optional*|This is the exchange on which the order should preferably be placed.|string||
|**Query**|**userId**  <br>*optional*|Post on behalf of another user, optional admin feature|integer (int32)|`0`|
|**Body**|**body**  <br>*required*|This is JSON data that contains information about the new order.|[CreateOrderResource](#createorderresource)||


##### Responses

|HTTP Code|Description|Schema|
|---|---|---|
|**200**|JSON data with the order information is returned, indicating that the order has been successfully placed on the platform.|[OrderResource](#orderresource)|
|**401**|The access level of the provided authorization token is not sufficient to perform this operation.|No Content|
|**403**|The provided Et-App-Key is incorrect.|No Content|
|**422**|A validation error occurred while processing the request.|No Content|
|**500**|Internal server error|No Content|


##### Consumes

* `application/json`
* `text/json`


##### Produces

* `application/json`
* `text/json`



