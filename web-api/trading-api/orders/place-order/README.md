---
description: Place a new order
---

# Place Order

## Overview

This POST endpoint enables you to place a new order in AutoShares. The order is sent in the JSON format to our service which turns it into a new outstanding order that should eventually be fulfilled.

There are five required parameters that must be provided in the request:

1. **Et-App-Key** (header). This is the unique key of your app that identifies your app when communicating with our service. Contact your administrator to get this key.
2. **Authorization** (header). This is the authorization token from the very first [token request](../../authentication/requesting-tokens/). The value of this header must have the following format: `Bearer BQ898r9fefi` (`Bearer` + 1 space + the token).
3. **Trading Account ID** (path). This is the numeric ID of the trading account on which a new order must be placed.&#x20;
4. **API version** (path). Unless necessary, leave it at "1.0".
5. **body** (body of the request). This is a JSON file that contains the order's characteristics.&#x20;

Here's the final template for this API request:

* For orders that will only be verified by the API but not the execution venue (quick):

```
POST apiURL/v1.0/accounts/{accountID}/orders
```

* For orders that will be verified by the API and the execution venue too (slow):

```
POST apiURL/v1.0/accounts/{accountID}/syncorders
```

## Request Body

The body of this request represents the information about the to-be-created order. It must be sent in the JSON format with the parameters described in the following table:

| Parameter               | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| ----------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Symbol                  | This is the ticker symbol of the underlying security in the new order.                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| ClientId                | This is the order ID on the client's side.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| ExpireDate              | This is the expiration of the order. If the order isn't executed until the specified date, it'll automatically be cancelled.                                                                                                                                                                                                                                                                                                                                                                                                      |
| Type                    | This is the type of the order. The range of possible values includes: **Market**, **Limit**, **Stop**, **Stop Limit**.                                                                                                                                                                                                                                                                                                                                                                                                            |
| Side                    | This is the side of the trade. The range of possible values includes: **Buy**, **Sell**, **SellShort**, **BuyToCover**.                                                                                                                                                                                                                                                                                                                                                                                                           |
| ExecInst                | Indicates if the order should be filled either entirely in one transaction or not at all. Possible value: **'AllOrNone'**.                                                                                                                                                                                                                                                                                                                                                                                                        |
| TimeInforce             | <p>Indicates the time frame in which the order will be active. Possible Values:</p><ol><li><strong>Day</strong>. The order automatically expires at the end of the regular trading session if it weren't executed.</li><li><strong>GoodTillCancel</strong> (Good-till-Canceled). The order persists indefinitely until it is executed or manually cancelled.</li><li><strong>GoodTillDate</strong>. The order will be active until the date specified in the ExpireDate attribute (unless it is executed or cancelled).</li></ol> |
| Quantity                | The number of shares in the order.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| Price                   | The price at which the shares must be purchased.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| StopPrice               | When this price is reached, the order will automatically be converted into a market order.                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| Exchange                | This is the exchange on which the order should be executed.                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| TrailingStopAmountType  | This is the type of the trailing stop (**Absolute** or **Persentage**).                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| TrailingStopAmount      | This is the trailing amount of the trailing stop (in percentage terms or in the currency units).                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| TrailingLimitAmountType | This is the type of the trailing limit (**Absolute** or **Persentage**).                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| TrailingLimitAmount     | This is the trailing amount (in percentage terms or in the currency units).                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| ExtendedHours           | Indicates if the order should be placed during the extended hours (pre-market session, post-market session).                                                                                                                                                                                                                                                                                                                                                                                                                      |
| ExecutionInstructions   | <p></p><p>Execution instructions of the order. May include the following data:</p><ul><li><code>"PerTradeCommission": "1"</code>. Specified in <strong>dollars</strong> ($1 per trade).</li><li><code>"PerContractCommission":"1"</code>. Specified in <strong>cents</strong> (1 cent per contract).</li></ul>                                                                                                                                                                                                                    |
| Legs                    | These are the legs of a multi-leg order.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |

```javascript
{
  "Symbol": "AAPL", //Buying 100 shares of the Apple stock
  "Type": "Market",
  "Side": "Buy",
  "Quantity": 100
}
```

### Smallest Limit Order Sample

```javascript
{
  "Symbol": "AAPL", //Buying 100 shares of the Apple stock
  "Type": "Limit",
  "Side": "Buy",
  "Quantity": 100,
  "Price" : 170 //The limit price of the order
}
```

### Smallest Stop Order Sample

```javascript
{
  "Symbol": "AAPL", //Buying 100 shares of the Apple stock
  "Type": "Stop",
  "Side": "Buy",
  "Quantity": 100,
  "StopPrice" : 150 //The stop price of the order
}
```

### Smallest Stop-Limit Order Sample

```javascript
{
  "Symbol": "AAPL", //Buying 100 shares of the Apple stock
  "Type": "StopLimit",
  "Side": "Buy",
  "Quantity": 100,
  "StopPrice" : 149, //The stop price of the order
  "Price": 150 //The limit price of the order
}
```

### Smallest Limit Order Sample (Options)

```javascript
{
  "Symbol": "STNE  190517P00055000", //the option's OSI Symbol
  "ExpireDate": "2019-03-24T17:32:28.824Z",
  "Type": "Limit",
  "Side": "Buy",
  "Price":170,
  "ExecInst": "AllOrNone",
  "TimeInforce": "Day",
  "Quantity": 1,
}
```

### Complex Order Sample (Options)

```javascript
{
  "Symbol": "AAPL  190503C00165000", //the option's OSI Symbol
  "ExpireDate": "2019-03-30T17:00:00.824Z",  
  "Type": "Limit",
  "Side": "Buy",
  "Price":170,
  "ExecInst": "AllOrNone",
  "TimeInforce": "Day",
  "Quantity": 1,
  "Legs": [{ //simultaneously buying the Apple stock
            "Symbol": "AAPL", 
            "Type": "Market",
            "Side": "Buy",
            "Quantity": 100
        }
    ]
}
```

### Multi-Leg Order Sample (Option + Option)

All legs of a multi-leg order should contain only three parameters:&#x20;

1. Ticker symbol
2. Quantity
3. Side

All other parameters like the order's type and limit price must be specified outside the legs as the root parameters applicable to all legs.

{% hint style="warning" %}
The type of a multi-leg order must be either **market** or **limit**.
{% endhint %}

```javascript
{
  "Legs": [
    {
      
      "Quantity": 2,
      "Side": "SellShort",
      "Symbol": "AAPL  200214C00327500",
      
    },
    {
      
      "Quantity": 2,
      "Side": "Buy",
      "Symbol": "AAPL  200214C00380000",
      
    }
  ],
  "ExecInst": "AllOrNone",
  "ExpireDate": "2020-11-04T08:44:17.738365+00:00",
  "Price": 0.5,
  "Quantity": 2,
  "Symbol": "",
  "TimeInForce": "Day",
  "Type": "Limit"
}
```

### Comprehensive Limit Order Sample

```javascript
{
  "Symbol": "AAPL",
  "ExpireDate": "2019-03-24T10:07:59.181Z",
  "Type": "Limit",
  "Side": "Buy",
  "ExecInst": "AllOrNone",
  "TimeInforce": "GoodTillCancel",
  "Quantity": 100,
  "Price": 190,
  "Exchange": "XNAS",
  "ExtendedHours": "REGPOST",
  "Comment": "Expecting a remarkable Q4 report",
  "ExecutionInstructions" : {"PerTradeCommission": "1", //Charging $1 for the entire transaction
                             "PerContractCommission":"1"}, //Charging 1 cent for each stock
}
```

### Comprehensive Market Order Sample

```javascript
{
  "Symbol": "AAPL",
  "ExpireDate": "2019-03-24T10:07:59.181Z",
  "Type": "Market",
  "Side": "Buy",
  "ExecInst": "AllOrNone",
  "TimeInforce": "GoodTillCancel",
  "Quantity": 445,
  "Exchange": "XNAS",
  "ExtendedHours": "PRE",
  "ExecutionInstructions" : {"PerTradeCommission": "1", //Charging $1 for the entire transaction
                             "PerContractCommission":"1"}, //Charging 1 cent for each stock
}
```

### Comprehensive Stop Order Sample

```javascript
{
  "Symbol": "AAPL",
  "ExpireDate": "2019-07-30T10:07:59.181Z",
  "Type": "Stop",
  "Side": "Buy",
  "ExecInst": "AllOrNone",
  "TimeInforce": "GoodTillCancel",
  "Quantity": 100,
  "StopPrice" : 200,
  "Exchange": "XNAS",
  "ExtendedHours": "REG",
  "ExecutionInstructions" : {"PerTradeCommission": "1", //Charging $1 for the entire transaction
                             "PerContractCommission":"1"}, //Charging 1 cent for each stock
}
```

### Comprehensive Stop Limit Order Sample

```javascript
{
  "Symbol": "AAPL",
  "ExpireDate": "2019-12-20T10:07:59.181Z",
  "Type": "StopLimit",
  "Side": "Buy",
  "ExecInst": "AllOrNone",
  "TimeInforce": "GoodTillCancel",
  "Quantity": 105,
  "Exchange": "XNAS",
  "ExtendedHours": "REGPOST",
  "Price" : 201,
  "StopPrice" : 200,
  "ExecutionInstructions" : {"PerTradeCommission": "1", //Charging $1 for the entire transaction
                             "PerContractCommission":"1"}, //Charging 1 cent for each stock
}
```

### Comprehensive Trailing Stop Order Type

```javascript
{
  "Symbol": "AAPL",
  "ExpireDate": "2019-12-20T10:07:59.181Z",
  "Type": "TrailingStop",
  "Side": "Buy",
  "ExecInst": "AllOrNone",
  "TimeInforce": "GoodTillCancel",
  "Quantity": 105,
  "Exchange": "XNAS",
  "ExtendedHours": "REGPOST",
  "TrailingStopAmountType" : "Persentage",
  "TrailingStopAmount" : 2,
  "ExecutionInstructions" : {"PerTradeCommission": "1", //Charging $1 for the entire transaction
                             "PerContractCommission":"1"}, //Charging 1 cent for each stock
}
```

### Comprehensive Trailing Stop Limit Order Type

```javascript
{
  "Symbol": "AAPL",
  "ExpireDate": "2019-12-20T10:07:59.181Z",
  "Type": "TrailingStopLimit",
  "Side": "Buy",
  "ExecInst": "AllOrNone",
  "TimeInforce": "GoodTillCancel",
  "Quantity": 1,
  "Exchange": "XNAS",
  "TrailingLimitAmountType" : "Absolute", //Limit offset
  "TrailingLimitAmount" : 4,
  "ExtendedHours": "REGPOST",
  "TrailingStopAmountType" : "Absolute", //Trailing Stop
  "TrailingStopAmount" : 10,
  "ExecutionInstructions" : {"PerTradeCommission": "1", //Charging $1 for the entire transaction
                             "PerContractCommission":"1"}, //Charging 1 cent for each stock
}
```

### One-Triggers-the-Other Order Type

One-Triggers-the-Other is a type of conditional order in which execution of one order automatically triggers the other one. Each of the two orders has to be provided as a separate leg:

```javascript
{
    "Type": "OneTriggerOther", //the type of the order
        "Symbol": "", //this parameter must be empty
        "Legs": [{ //the array of two legs
            "Symbol": "AAPL", //the first leg
            "Type": "Limit",
            "Price": 150,
            "Side": "Buy",
            "Quantity": 100
        },
        {
            "Symbol": "TSLA", //the second leg
            "Type": "Limit",
            "Price": 100,
            "Side": "Buy",
            "Quantity": 100
        }
    ]
}
```

In this case, if the limit order to purchase the Apple stock gets executed, the second limit order to purchase the Tesla stock will automatically be triggered.

{% hint style="warning" %}
In One-Triggers-the-Other orders, the first leg cannot be a market order.
{% endhint %}

### One-Cancels-the-Other Order Type

One-Cancels-the-Other is a type of conditional order in which execution of one order automatically cancels the other one. Each of the two orders has to be provided as a separate leg:

```javascript
{
    "Type": "OneCancelOther", //the type of the order
        "Symbol": "", //this parameter must be empty
        "Legs": [{ //the array of two legs
            "Symbol": "AAPL", //the first leg
            "Type": "Limit",
            "Price": 150,
            "Side": "Buy",
            "Quantity": 100
        },
        {
            "Symbol": "TSLA", //the second leg
            "Type": "Limit",
            "Price": 100,
            "Side": "Buy",
            "Quantity": 100
        }
    ]
}
```

In this case, if the limit order to purchase the Apple stock gets executed, the second limit order to purchase the Tesla stock will automatically be cancelled.

{% hint style="warning" %}
In One-Cancels-the-Other orders, both legs cannot be market orders.
{% endhint %}

## Response

In response to this request, you'll receive a JSON file with comprehensive information about the newly created order:

```javascript
{
    "Id": 80328,
    "SecurityId": 4,
    "Quantity": 100,
    "Price": 0,
    "StopPrice": 0,
    "ClientId": "2029837977",
    "ExecutedQuantity": 0,
    "LastPrice": 0,
    "LastQuantity": 0,
    "LeavesQuantity": 0,
    "AveragePrice": 0,
    "Side": "Buy",
    "Date": "2019-02-25T13:33:40.9022856Z",
    "TransactionDate": "2019-02-25T13:33:40.9022856Z",
    "SettDate": "0001-01-01T00:00:00Z",
    "Status": "PendingNew",
    "ExecutionStatus": "PendingNew",
    "Type": "Market",
    "RequestStatus": "RequireValidation",
    "Target": "New",
    "TimeInForce": "Day",
    "ExecInst": 0,
    "Comment": "Expecting a remarkable Q4 report",
    "ExpireDate": "2019-02-25T21:00:00Z",
    "AccountId": 6303,
    "UserId": 7125,
    "RequestId": 105467,
    "StateId": 0,
    "ParentId": -1,
    "Legs": [],
    "TrailingStopAmountType": "Absolute",
    "TrailingStopAmount": 0,
    "TrailingLimitAmountType": "Absolute",
    "TrailingLimitAmount": 0,
    "CreateDate": "2019-02-25T13:33:40.9022856Z",
    "InitialType": "Market",
    "IsExternal": false,
    "ExecutionInstructions": {
        "CorrelationId": "ade9537995f84dcc840eabc724107487",
        "CreateOrderRequestTimeUnix": "636866984209012879"
    },
    "TransType": "New",
    "ValidationsToBypass": 0,
    "ParentRequestId": 0,
    "SettlementDate": "0001-01-01T00:00:00Z"
}
```

{% hint style="warning" %}
Please note that you may receive the 200 status code even if the order was improperly configured. For example, if you attempt to create a limit order and specify the stop price instead of the limit price, the order will be registered in the system but will eventually be rejected. Please monitor the order's status (it's _PendingNew_ by default) to determine if the order has been rejected or placed.
{% endhint %}

## Common Mistakes

Here are some of the common mistakes that developers make when attempting to place a new order.

### Failing to Specify the Et-App-Key Parameter

If you specify the wrong Et-App-Key parameter or fail to include it in the header altogether, you'll get the following error:

```javascript
{
    "error": "Application key is not defined or does not exist"
}
```

### Specifying the User ID Instead of the Trading Account ID

Another common mistake when making this request is specifying the user ID instead of the user's trading account ID. Doing so will result in the 500 status code and the following error message:

```javascript
{
    "message": "An error occurred while processing your request",
    "error": "Unexpected server error"
}
```

### Specifying a Trading Account of a Different User

It's critical to understand that when you use the authorization token of a particular user in this request's header, only this user's trading accounts can be used for placing new orders. Placing a new order on a trading account of a different user will lead to the 401 error.

```javascript
{
    "Message": "Authorization has been denied for this request."
}
```

In the following article we provide in-depth coverage of the syntax for this API request.

### Placing Orders Whose Value Exceeds the Account's Buying Power

When attempting to place an order whose value exceeds the trading account's buying power, you'll receive a JSON file with the `ErrorDescription` parameter equaling `DayTradingBuyingPowerExceeded`.

```javascript
{
  "IsSuccessful": false,
  "ErrorDescription": "DayTradingBuyingPowerExceeded",
  "ErrorDescriptionArgs": [],
  "Commission": 3.75,
  "Commissions": {
    "Per Trade Commission": 3.75
  },
  "Cost": 1766790,
  "NetCost": 1766786.25,
  "Quotes": [
    {
      "Ask": 196.31,
      "Bid": 196.28,
      "Last": 196.29,
      "Volume": 200,
      "OpenInterest": 0
    }
  ],
  "MarginChange": 0
}
```

### Failing to Specify the Limit Price for Limit Orders

An attempt to place a limit order without specifying its price will result in an error; in response you'll receive a JSON file with the `ErrorDescription` parameter equaling `QuotePriceIsInvalid`.

```javascript
{
  "IsSuccessful": false,
  "ErrorDescription": "QuotePriceIsInvalid",
  "Commission": 0,
  "Commissions": {},
  "Cost": 0,
  "NetCost": 0,
  "MarginChange": 0
}
```

### Failing to Specify the Stop Price for Stop-Loss Orders

An attempt to place a stop-loss order without specifying its price will result in an error; in response you'll receive a JSON file with the `ErrorDescription` parameter equaling `QuotePriceIsInvalid`.

```javascript
{
  "IsSuccessful": false,
  "ErrorDescription": "QuotePriceIsInvalid",
  "Commission": 0,
  "Commissions": {},
  "Cost": 0,
  "NetCost": 0,
  "MarginChange": 0
}
```

## Sample Code

Feel free to examine our [Code Samples](../../code-samples/placing-new-orders.md#placing-new-orders-and-checking-their-status) article that demonstrates how to place a new order with the help of a Python script.

The following article covers the syntax for this API request in detail.
