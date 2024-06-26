---
description: Validate a new order before placing it
---

# Validate Order Placement

### Overview

This POST endpoint enables you to validate an order before placing it in AutoShares. This might be useful for ensuring that the user has properly constructed an order and prevent any issues related with defective orders.

There are five required parameters that must be provided in the request:

1. **Et-App-Key** \(header\). This is the unique key of your app that identifies your app when communicating with our service. Contact your administrator to get this key.
2. **Authorization** \(header\). This is the authorization token from the very first [token request](../../authentication/).
3. **API version** \(path\). Unless necessary, leave it at "1.0".
4. **Trading Account ID** \(path\). This is the numeric ID of the trading account on which an existing order replacement must be validated.
5. **placeParams** \(body\). This is a JSON file that contains the parameters of a new order that must be validated.

Here's the final template for this API request:

```text
POST apiURL/v1.0/accounts/{accountID}/preview/orders
```

### Request Body

The body of this request represents the information of the new order that must be validated before you can proceed to place it. The order must be sent in the JSON format with mandatory parameters about the order.

<table>
  <thead>
    <tr>
      <th style="text-align:left">Parameter</th>
      <th style="text-align:left">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">Symbol</td>
      <td style="text-align:left">This is the ticker symbol of the underlying security in the new order.</td>
    </tr>
    <tr>
      <td style="text-align:left">ClientId</td>
      <td style="text-align:left">This is the order ID on the client&apos;s side.</td>
    </tr>
    <tr>
      <td style="text-align:left">ExpireDate</td>
      <td style="text-align:left">This is the expiration of the order. If the order isn&apos;t executed
        until the specified date, it&apos;ll automatically be cancelled.</td>
    </tr>
    <tr>
      <td style="text-align:left">Type</td>
      <td style="text-align:left">This is the type of the order. The range of possible values includes: <b>Market</b>, <b>Limit</b>, <b>Stop</b>, <b>Stop Limit</b>.</td>
    </tr>
    <tr>
      <td style="text-align:left">Side</td>
      <td style="text-align:left">This is the side of the trade. The range of possible values includes: <b>Buy</b>, <b>Sell</b>, <b>Sell</b>  <b>Short</b>, <b>Buy to Cover</b>.</td>
    </tr>
    <tr>
      <td style="text-align:left">ExecInst</td>
      <td style="text-align:left">Indicates if the order should be filled either entirely in one transaction
        or not at all. Possible values: <b>&apos;DoNotIncrease&apos;</b>, <b>&apos;DoNotReduce&apos;</b>, <b>&apos;AllOrNone&apos;</b>.</td>
    </tr>
    <tr>
      <td style="text-align:left">TimeInforce</td>
      <td style="text-align:left">
        <p>Indicates the time frame in which the order will be active. Possible Values:</p>
        <ol>
          <li><b>Day</b>. The order automatically expires at the end of the regular
            trading session if it weren&apos;t executed.</li>
          <li><b>GTC </b>(Good-till-Canceled). The order persists indefinitely until
            it is executed or manually cancelled.</li>
          <li><b>AtTheOpening</b>. The order should be filled at the opening of the
            marketplace or cancelled.</li>
          <li><b>ImmediateOrCancel</b>. The order should be completely or partially
            filled immediately. If partially filled, the remaining part of the order
            should be cancelled.</li>
          <li><b>FillOrKill</b>. The order should be filled immediately and entirely
            or cancelled right away.</li>
          <li><b>GoodTillCrossing</b>. The order will be active until the market enters
            the auction phase.</li>
          <li><b>GoodTillDate</b>. The order will be active until the date specified
            in the ExpireDate attribute (unless it is executed or cancelled).</li>
          <li><b>GoodTillTime</b>. The order will be active until a certain time point.</li>
        </ol>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Quantity</td>
      <td style="text-align:left">The number of shares in the order.</td>
    </tr>
    <tr>
      <td style="text-align:left">Price</td>
      <td style="text-align:left">The price at which the shares must be purchased.</td>
    </tr>
    <tr>
      <td style="text-align:left">StopPrice</td>
      <td style="text-align:left">When this price is reached, the order will automatically be converted
        into a market order.</td>
    </tr>
    <tr>
      <td style="text-align:left">Exchange</td>
      <td style="text-align:left">This is the exchange on which the order should be executed.</td>
    </tr>
    <tr>
      <td style="text-align:left">TrailingStopAmountType</td>
      <td style="text-align:left">This is the type of the trailing stop (<b>Absolute</b> or <b>Persentage</b>).</td>
    </tr>
    <tr>
      <td style="text-align:left">TrailingStopAmount</td>
      <td style="text-align:left">This is the trailing amount of the trailing stop (in percentage terms
        or in the currency units).</td>
    </tr>
    <tr>
      <td style="text-align:left">TrailingLimitAmountType</td>
      <td style="text-align:left">This is the type of the trailing limit (<b>Absolute</b> or <b>Persentage</b>).</td>
    </tr>
    <tr>
      <td style="text-align:left">TrailingLimitAmount</td>
      <td style="text-align:left">This is the trailing amount (in percentage terms or in the currency units).</td>
    </tr>
    <tr>
      <td style="text-align:left">ExtendedHours</td>
      <td style="text-align:left">Indicates if the order should be placed during the extended hours (pre-market
        session, post-market session).</td>
    </tr>
    <tr>
      <td style="text-align:left">ExecutionInstructions</td>
      <td style="text-align:left">Execution instructions for algorithmic trades.</td>
    </tr>
    <tr>
      <td style="text-align:left">Legs</td>
      <td style="text-align:left">These are the legs of a multi-leg order.</td>
    </tr>
  </tbody>
</table>The first four parameters — **Symbol**, **Quantity**, **Type**, and **Side** — are mandatory, while the remaining parameters should only be provided if necessary.

#### Smallest Market Order Validation Sample

```javascript
{
  "Symbol": "AAPL", //Buying 100 shares of the Apple stock
  "Type": "Market",
  "Side": "Buy",
  "Quantity": 100
}
```

#### Smallest Limit Order Validation Sample

```javascript
{
  "Symbol": "AAPL", //Buying 100 shares of the Apple stock
  "Type": "Limit",
  "Side": "Buy",
  "Quantity": 100,
  "Price" : 170 //The limit price of the order
}
```

#### Smallest Stop Order Validation Sample

```javascript
{
  "Symbol": "AAPL", //Buying 100 shares of the Apple stock
  "Type": "Stop",
  "Side": "Buy",
  "Quantity": 100,
  "StopPrice" : 150 //The stop price of the order
}
```

#### Smallest Stop-Limit Order Validation Sample

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

#### Option-Buying Limit Order Validation Sample

```javascript
{
  "Symbol": "STNE  190517P00055000", //the ID of the purchased option
  "ExpireDate": "2019-03-24T17:32:28.824Z",
  "Type": "Limit",
  "Side": "Buy",
  "Price":170,
  "ExecInst": "DoNotIncrease",
  "TimeInforce": "Day",
  "Quantity": 1,
}
```

#### Complex Option-Buying Order Validation Sample

```javascript
{
  "Symbol": "AAPL  190503C00165000", //buying an Apple stock option
  "ExpireDate": "2019-03-30T17:00:00.824Z",  
  "Type": "Limit",
  "Side": "Buy",
  "Price":170,
  "ExecInst": "DoNotIncrease",
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

#### Comprehensive Limit Order Validation Sample

```javascript
{
  "Symbol": "AAPL",
  "ExpireDate": "2019-03-24T10:07:59.181Z",
  "Type": "Limit",
  "Side": "Buy",
  "ExecInst": "AllOrNone",
  "TimeInforce": "GTC",
  "Quantity": 100,
  "Price": 190,
  "Exchange": "XNAS",
  "ExtendedHours": "REGPOST"
}
```

#### Comprehensive Market Order Validation Sample

```javascript
{
  "Symbol": "AAPL",
  "ExpireDate": "2019-03-24T10:07:59.181Z",
  "Type": "Market",
  "Side": "Buy",
  "ExecInst": "AllOrNone",
  "TimeInforce": "GTC",
  "Quantity": 445,
  "Exchange": "XNAS",
  "ExtendedHours": "PRE"
}
```

#### Comprehensive Stop Order Validation Sample

```javascript
{
  "Symbol": "AAPL",
  "ExpireDate": "2019-07-30T10:07:59.181Z",
  "Type": "Stop",
  "Side": "Buy",
  "ExecInst": "AllOrNone",
  "TimeInforce": "GTC",
  "Quantity": 100,
  "StopPrice" : 200,
  "Exchange": "XNAS",
  "ExtendedHours": "REG"
}
```

#### Comprehensive Stop Limit Order Validation Sample

```javascript
{
  "Symbol": "AAPL",
  "ExpireDate": "2019-12-20T10:07:59.181Z",
  "Type": "StopLimit",
  "Side": "Buy",
  "ExecInst": "AllOrNone",
  "TimeInforce": "GTC",
  "Quantity": 105,
  "Exchange": "XNAS",
  "ExtendedHours": "REGPOST",
   "Price" : 201,
   "StopPrice" : 200
}
```

#### Comprehensive Trailing Stop Order Validation Type

```javascript
{
  "Symbol": "AAPL",
  "ExpireDate": "2019-12-20T10:07:59.181Z",
  "Type": "TrailingStop",
  "Side": "Buy",
  "ExecInst": "AllOrNone",
  "TimeInforce": "GTC",
  "Quantity": 105,
  "Exchange": "XNAS",
  "ExtendedHours": "REGPOST",
  "TrailingStopAmountType" : "Persentage",
  "TrailingStopAmount" : 2
}
```

#### Comprehensive Trailing Stop Limit Order Validation Type

```javascript
{
  "Symbol": "AAPL",
  "ExpireDate": "2019-12-20T10:07:59.181Z",
  "Type": "TrailingStopLimit",
  "Side": "Buy",
  "ExecInst": "AllOrNone",
  "TimeInforce": "GTC",
  "Quantity": 1,
  "Exchange": "XNAS",
  "TrailingLimitAmountType" : "Absolute", //Limit offset
  "TrailingLimitAmount" : 4,
  "ExtendedHours": "REGPOST",
  "TrailingStopAmountType" : "Absolute", //Trailing Stop
  "TrailingStopAmount" : 10,
}
```

#### One-Triggers-the-Other Order Validation Type

One-Triggers-the-Other is a type of conditional order in which execution of one order automatically triggers the other one. Each of the two orders has to be provided as a separate leg:

```javascript
{
	"Type": "OneTriggerOther", //the type of the order
        "Symbol": "AAPL",
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

#### One-Cancels-the-Other Order Validation Type

One-Cancels-the-Other is a type of conditional order in which execution of one order automatically cancels the other one. Each of the two orders has to be provided as a separate leg:

```javascript
{
	"Type": "OneCancelOther", //the type of the order
        "Symbol": "AAPL",
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

#### One-Triggers-OCO Order Validation Type

One-Triggers-OCO is a type of conditional order in which execution of one order triggers execution of a One-Cancels-the-Other order. This order type is useful in strategies where you purchase a security \(trigger\) and then automatically configure a stop-loss and a take-profit order \(OCO\). The first order — the trigger — is provided as the first leg while the OCO order is provided as the second and the third legs.

```javascript
{
	"Type": "OneTriggerOneCancelOther",
	"Symbol": "AAPL",
	"Legs": [{
			"Symbol": "AAPL", //the trigger order — the first leg
			"Type": "Limit",
			"Side": "Buy",
			"Price": 190,
			"Quantity": 100
		},
		{
			"Symbol": "AAPL", //the first leg of the OCO order 
			"Type": "Limit",
			"Price": 200,
			"Side": "Sell",
			"Quantity": 100
		},
		{
			"Symbol": "AAPL", //the second leg of the OCO order 
			"Type": "Stop",
			"StopPrice": 189,
			"Side": "Sell",
			"Quantity": 100
		}
	]
}
```

### Response

In response to this request, you'll receive a JSON file confirming \(or rejecting\) that the new order has been properly constructed.

```javascript
{
  "IsSuccessful": true,
  "Commission": 3.75,
  "Commissions": {
    "Per Trade Commission": 3.75
  },
  "Cost": 169000,
  "NetCost": 168996.25,
  "Quotes": [
    {
      "Ask": 184,
      "Bid": 175.76,
      "Last": 175.875,
      "Volume": 1,
      "OpenInterest": 0
    }
  ],
  "MarginChange": 16900
}
```

where:

| Parameter | Description |
| :--- | :--- |
| IsSuccessful | This field indicates if the order has been successfully constructed. |
| Commission | This is the total commission applicable to the order. |
| Commissions | This is an array that breaks down the applicable commissions. |
| Cost | This is the total cost of the order \(including commission\). |
| NetCost | This is the cost of the order less commission. |
| Quotes | This is the last batch of quotes for this security. |
| MarginChange | This is the amount by which the trading account margin requirements will be affected once this order is filled. |
| ErrorDescription | This is the description of the error in case the provided order was improperly constructed. |
| ErrorDescriptionArgs | This is an array with error description arguments. |

### Common Mistakes

Here are some of the common mistakes that developers make when attempting to validate a new order.

#### Failing to Specify the Et-App-Key Parameter

If you specify the wrong Et-App-Key parameter or fail to include it in the header altogether, you'll get the following error:

```javascript
{
    "error": "Application key is not defined or does not exist"
}
```

#### Providing an Incorrect Set of Parameters 

Another common mistake made when sending this API request is failing to provide all mandatory parameters. Doing so will result in the 500 status code and the following error message:

```javascript
{
  "message": "An error occurred while processing your request",
  "error": "Unexpected server error"
}
```

### 

