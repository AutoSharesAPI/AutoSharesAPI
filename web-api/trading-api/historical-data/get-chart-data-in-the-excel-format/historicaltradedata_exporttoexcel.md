# Syntax

## Get excel file with chart data

```
POST /v{version}/history/export
```

### Description

Get excel file with chart data

### Parameters

| Type       | Name                                                       | Description                                                                                                                          | Schema                                                                                                         | Default |
| ---------- | ---------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------ | -------------------------------------------------------------------------------------------------------------- | ------- |
| **Header** | <p><strong>Authorization</strong><br><em>required</em></p> | This is the authorization token that you retrieved from the first endpoint (/token).                                                 | string                                                                                                         |         |
| **Path**   | <p><strong>version</strong><br><em>required</em></p>       | This is the version of the API. Unless you have multiple versions of AutoShares’s API deployed in your environment, leave it at 1.0. | string                                                                                                         | `"1"`   |
| **Body**   | <p><strong>body</strong><br><em>required</em></p>          |                                                                                                                                      | [HistoricalTradeDataExportDataModel](historicaltradedata\_exporttoexcel.md#historicaltradedataexportdatamodel) |         |

### Responses

| HTTP Code | Description                                                                                       | Schema     |
| --------- | ------------------------------------------------------------------------------------------------- | ---------- |
| **200**   | Requested excel file with chart data                                                              | object     |
| **401**   | The access level of the provided authorization token is not sufficient to perform this operation. | No Content |
| **422**   | A validation error occurred while processing the request.                                         | No Content |
| **500**   | Internal server error                                                                             | No Content |

### Consumes

* `application/json`
* `text/json`

### Produces

* `application/json`
* `text/json`
