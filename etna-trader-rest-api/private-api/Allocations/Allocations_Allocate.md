
<a name="allocations_allocate"></a>
#### Create multileg allocation request
```
PUT /v{version}/allocations/multileg
```


##### Description
Executes single trade multileg allocation request


##### Parameters

|Type|Name|Description|Schema|Default|
|---|---|---|---|---|
|**Header**|**Authorization**  <br>*required*|Bearer type token string|string||
|**Header**|**Et-App-Key**  <br>*required*|Application key|string||
|**Path**|**version**  <br>*required*|The requested API version|string|`"1"`|
|**Body**|**body**  <br>*required*|Allocation request model|[MultilegAllocationRequest](#multilegallocationrequest)||


##### Responses

|HTTP Code|Description|Schema|
|---|---|---|
|**200**|Succeeded allocation request result|[AllocationResultInfo[MultilegAllocationRequest]](#allocationresultinfo-multilegallocationrequest)|
|**401**|Authorization has been denied for this request.|No Content|
|**403**|Application key is not defined or does not exist|No Content|
|**409**|Failed allocation request result|[AllocationResultInfo[MultilegAllocationRequest]](#allocationresultinfo-multilegallocationrequest)|
|**422**|Validation error occurred while processing entity|No Content|
|**500**|Internal server error|No Content|


##### Consumes

* `application/json`
* `text/json`


##### Produces

* `application/json`
* `text/json`


