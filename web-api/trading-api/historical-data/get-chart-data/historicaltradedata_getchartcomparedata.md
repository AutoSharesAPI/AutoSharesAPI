# Syntax

## Get chart compare data

```
PUT /v{version}/history/compare
```

### Description

This API endpoint enables you to retrieve and compare historical chart data for a set of securities. This data includes price ranges, candles, and various other non-market data.

### Parameters

| Type       | Name                                                       | Description                                                                                                                          | Schema                                                                                           | Default |
| ---------- | ---------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------ | ------- |
| **Header** | <p><strong>Authorization</strong><br><em>required</em></p> | This is the authorization token that you retrieved from the first endpoint (/token).                                                 | string                                                                                           |         |
| **Path**   | <p><strong>version</strong><br><em>required</em></p>       | This is the version of the API. Unless you have multiple versions of AutoShares’s API deployed in your environment, leave it at 1.0. | string                                                                                           | `"1"`   |
| **Body**   | <p><strong>body</strong><br><em>required</em></p>          | This is a JSON dictionary that contains information about the specified securities.                                                  | [ChartCompareRequestModel](historicaltradedata\_getchartcomparedata.md#chartcomparerequestmodel) |         |

### Responses

| HTTP Code | Description                                                                                                | Schema                                                                                                                         |
| --------- | ---------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------ |
| **200**   | Successful request, JSON data is returned, containing the chart data for the list of specified securities. | < < [TimeSeriesValueCandleMapModel](historicaltradedata\_getchartcomparedata.md#timeseriesvaluecandlemapmodel) > array > array |
| **401**   | The access level of the provided authorization token is not sufficient to perform this operation.          | No Content                                                                                                                     |
| **409**   | Chart data cannot be provided                                                                              | No Content                                                                                                                     |
| **422**   | A validation error occurred while processing the request.                                                  | No Content                                                                                                                     |
| **500**   | Internal server error                                                                                      | No Content                                                                                                                     |

### Consumes

* `application/json`
* `text/json`

### Produces

* `application/json`
* `text/json`
