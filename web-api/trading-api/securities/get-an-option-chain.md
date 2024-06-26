# Get an Option Chain

## Overview

This GET endpoint enables you to retrieve an option chain for a specific security. An option chain is a series of options with a fixed number of options with the strike price above and below a center strike price. For instance, if you want an option chain with `Range` set to `1`, you will receive two pairs (Call + Put) of options: one above the center strike price and another below the center strike price.

There are four required parameters that must be provided in the request's header and query:

1. **Authorization** (header). This is the authorization token from the very first [token request](broken-reference). The value of this header must have the following format: `Bearer BQ898r9fefi` (`Bearer` + 1 space + the token).
2. **API version** (path). Unless necessary, leave it at "1.0".
3. **symbol** (path). This is the ticker symbol of the underlying security for which the option series must be fetched.

There's also one optional parameter worth examining:

* filter (query). This is an SQL query used to retrieve only those options that satisfy the conditions of the query. The following table outlines the parameter's syntax.

| Syntax                                | Description                                                                                                                                                                                                                                                                                                     | Example                                               |
| ------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------- |
| <ul><li>Expiration = {Date}</li></ul> | This query enables you to retrieve options with a specific expiration date.                                                                                                                                                                                                                                     | <ul><li>Expiration = #2020-01-17T00:00:00Z#</li></ul> |
| <ul><li>Range = {integer}</li></ul>   | This query enables you to retrieve the specified number of options below and above the center strike price. For instance, if you want an option chain with `Range` set to `1`, you will receive two pairs (Call + Put) of options: one above the center strike price and another below the center strike price. | <ul><li>Range = 1</li></ul>                           |
| <ul><li>ExpirationType</li></ul>      | <p>This query enables you to retrieve options of the specified expiration type.</p><ul><li>Regular = 0</li><li>Quarterly = 1</li><li>Weekly = 2</li><li>Flex = 3</li><li>Undefined = 4</li><li>Mini = 5</li><li>NonStandard = 6</li></ul>                                                                       | <ul><li>ExpirationType = 0</li></ul>                  |

Here's the final template for this API request:

```
GET apiURL/v1.0/options/optionChain/AAPL?filter=Range%20%3D%201%20
```

### Response

In response to this API request, you will receive an option chain filtered according to the specified query:

```
{
  "Expirations": [
    {
      "Expiration": "2020-09-18T00:00:00Z",
      "CentralStrike": 320,
      "Options": [
        {
          "Id": 19358441,
          "Symbol": "AAPL  200918C00320000",
          "Description": "CALL Apple Inc. $320 EXP 09/18/20",
          "Exchange": "OPRAC",
          "Currency": "USD",
          "AddedDate": "2019-08-02T16:31:52.7125148Z",
          "ModifyDate": "2019-10-29T13:13:44.6562343Z",
          "Type": "Option",
          "Precision": 2,
          "VolumePrecision": 0,
          "TickSize": 0.01,
          "Enabled": true,
          "AllowTrade": true,
          "AllowMargin": true,
          "AllowShort": true,
          "OptionType": "Call",
          "ExpirationType": "Regular",
          "ExpirationDate": "2020-09-18T00:00:00Z",
          "StrikePrice": 320,
          "SeriesId": 103,
          "UnderlyingAssetSymbol": "AAPL",
          "ContractSize": 100
        },
        {
          "Id": 20303472,
          "Symbol": "AAPL  200918C00320000",
          "Description": "CALL Apple Inc. $320 EXP 09/18/20",
          "Currency": "USD",
          "AddedDate": "2019-10-23T14:07:32.9789618Z",
          "ModifyDate": "2019-10-23T14:07:32.9789618Z",
          "Type": "Option",
          "Precision": 2,
          "VolumePrecision": 0,
          "TickSize": 0.01,
          "Enabled": true,
          "AllowTrade": true,
          "AllowMargin": true,
          "AllowShort": true,
          "OptionType": "Call",
          "ExpirationType": "Regular",
          "ExpirationDate": "2020-09-18T00:00:00Z",
          "StrikePrice": 320,
          "SeriesId": 103,
          "UnderlyingAssetSymbol": "AAPL",
          "ContractSize": 100
        },
        {
          "Id": 20303475,
          "Symbol": "AAPL  200918P00320000",
          "Description": "PUT Apple Inc. $320 EXP 09/18/20",
          "Currency": "USD",
          "AddedDate": "2019-10-23T14:07:32.9789618Z",
          "ModifyDate": "2019-10-23T14:07:32.9789618Z",
          "Type": "Option",
          "Precision": 2,
          "VolumePrecision": 0,
          "TickSize": 0.01,
          "Enabled": true,
          "AllowTrade": true,
          "AllowMargin": true,
          "AllowShort": true,
          "OptionType": "Put",
          "ExpirationType": "Regular",
          "ExpirationDate": "2020-09-18T00:00:00Z",
          "StrikePrice": 320,
          "SeriesId": 103,
          "UnderlyingAssetSymbol": "AAPL",
          "ContractSize": 100
        },
        {
          "Id": 19358441,
          "Symbol": "AAPL  200918C00320000",
          "Description": "CALL Apple Inc. $320 EXP 09/18/20",
          "Exchange": "OPRAC",
          "Currency": "USD",
          "AddedDate": "2019-08-02T16:31:52.7125148Z",
          "ModifyDate": "2019-10-29T13:13:44.6562343Z",
          "Type": "Option",
          "Precision": 2,
          "VolumePrecision": 0,
          "TickSize": 0.01,
          "Enabled": true,
          "AllowTrade": true,
          "AllowMargin": true,
          "AllowShort": true,
          "OptionType": "Call",
          "ExpirationType": "Regular",
          "ExpirationDate": "2020-09-18T00:00:00Z",
          "StrikePrice": 320,
          "SeriesId": 103,
          "UnderlyingAssetSymbol": "AAPL",
          "ContractSize": 100
        },
        {
          "Id": 19358443,
          "Symbol": "AAPL  200918P00320000",
          "Description": "PUT Apple Inc. $320 EXP 09/18/20",
          "Exchange": "OPRAC",
          "Currency": "USD",
          "AddedDate": "2019-08-02T16:31:52.7125148Z",
          "ModifyDate": "2019-10-29T13:13:44.6562343Z",
          "Type": "Option",
          "Precision": 2,
          "VolumePrecision": 0,
          "TickSize": 0.01,
          "Enabled": true,
          "AllowTrade": true,
          "AllowMargin": true,
          "AllowShort": true,
          "OptionType": "Put",
          "ExpirationType": "Regular",
          "ExpirationDate": "2020-09-18T00:00:00Z",
          "StrikePrice": 320,
          "SeriesId": 103,
          "UnderlyingAssetSymbol": "AAPL",
          "ContractSize": 100
        },
        {
          "Id": 19358443,
          "Symbol": "AAPL  200918P00320000",
          "Description": "PUT Apple Inc. $320 EXP 09/18/20",
          "Exchange": "OPRAC",
          "Currency": "USD",
          "AddedDate": "2019-08-02T16:31:52.7125148Z",
          "ModifyDate": "2019-10-29T13:13:44.6562343Z",
          "Type": "Option",
          "Precision": 2,
          "VolumePrecision": 0,
          "TickSize": 0.01,
          "Enabled": true,
          "AllowTrade": true,
          "AllowMargin": true,
          "AllowShort": true,
          "OptionType": "Put",
          "ExpirationType": "Regular",
          "ExpirationDate": "2020-09-18T00:00:00Z",
          "StrikePrice": 320,
          "SeriesId": 103,
          "UnderlyingAssetSymbol": "AAPL",
          "ContractSize": 100
        },
        {
          "Id": 20303472,
          "Symbol": "AAPL  200918C00320000",
          "Description": "CALL Apple Inc. $320 EXP 09/18/20",
          "Currency": "USD",
          "AddedDate": "2019-10-23T14:07:32.9789618Z",
          "ModifyDate": "2019-10-23T14:07:32.9789618Z",
          "Type": "Option",
          "Precision": 2,
          "VolumePrecision": 0,
          "TickSize": 0.01,
          "Enabled": true,
          "AllowTrade": true,
          "AllowMargin": true,
          "AllowShort": true,
          "OptionType": "Call",
          "ExpirationType": "Regular",
          "ExpirationDate": "2020-09-18T00:00:00Z",
          "StrikePrice": 320,
          "SeriesId": 103,
          "UnderlyingAssetSymbol": "AAPL",
          "ContractSize": 100
        },
        {
          "Id": 20303475,
          "Symbol": "AAPL  200918P00320000",
          "Description": "PUT Apple Inc. $320 EXP 09/18/20",
          "Currency": "USD",
          "AddedDate": "2019-10-23T14:07:32.9789618Z",
          "ModifyDate": "2019-10-23T14:07:32.9789618Z",
          "Type": "Option",
          "Precision": 2,
          "VolumePrecision": 0,
          "TickSize": 0.01,
          "Enabled": true,
          "AllowTrade": true,
          "AllowMargin": true,
          "AllowShort": true,
          "OptionType": "Put",
          "ExpirationType": "Regular",
          "ExpirationDate": "2020-09-18T00:00:00Z",
          "StrikePrice": 320,
          "SeriesId": 103,
          "UnderlyingAssetSymbol": "AAPL",
          "ContractSize": 100
        }
      ]
    }
  ]
}
```

## Common Mistakes

Here are some of the common mistakes that developers make when attempting to retrieve option chains.
