---
description: Verify placing an exchange order for a mutual fund
---

# Verify Exchanging a Mutual Fund

### Overview

This POST endpoint enables you to verify an exchange order before placing it in AutoShares. This might be useful for ensuring that the user has properly constructed an order and prevent any issues related with defective orders.

There are five required parameters that must be provided in the request:

1. **Et-App-Key** \(header\). This is the unique key of your app that identifies your app when communicating with our service. Contact your administrator to get this key.
2. **Authorization** \(header\). This is the authorization token from the very first [token request](../../authentication/requesting-tokens/). The value of this header must have the following format: `Bearer BQ898r9fefi` \(`Bearer` + 1 space + the token\).
3. **Trading Account ID** \(path\). This is the internal ID of the trading account on whose behalf a new order must be placed. 
4. **API version** \(path\). Unless necessary, leave it at "1.0".
5. **body** \(body of the request\). This is a JSON object that contains the order's parameter.

#### Body Syntax

The body of this request represents the information about the verified order. It must be sent in the JSON format with the parameters described in the following table:

| Parameter | Description |
| :--- | :--- |
| SourceSymbol | The ticker symbol of the mutual fund that is being exchanged. |
| TargetSymbol | The ticker symbol of the mutual fund that is to be received in exchange. |
| ReinvestDividends | Indicates if the target mutual fund's managers should reinvest dividends received from its holdings. |
| ReinvestShortTermGains | Indicates if the target mutual fund's managers should reinvest the realized short-term capital gains. |
| ReinvestLongTermGains | Indicates if the target mutual fund's managers should reinvest the realized short-term capital gains. |

The following is a sample JSON that can be used to verify a exchange order:

```javascript
{
    SourceSymbol: "FKINX",
    TargetSymbol: "SAAAX",
    ReinvestDividends: false,
    ReinvestLongTermGains: false,
    ReinvestShortTermGains: false
}
```

Here's the final template for this API request:

```text
POST apiURL/v1.0/accounts/{Trading Account ID}/preview/orders/mutual-funds/exchange
```

### Response

In response to this API request, you will receive a JSON object either confirming that the order is valid or rejecting it with an accompanying message \(look at the `IsSuccessful` parameter\):

```javascript
{ 
"IsSuccessful": false, 
"ErrorDescription": "AccountIsNotApproved", 
"ErrorDescriptionText": "Account is not approved for trading. Please contact our support team.", 
"ErrorDescriptionArgs": [] 
}
```

### Common Mistakes

Here are some of the common mistakes that developers make when attempting to verify an exchange order:

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
  "Message": "Validation error occured while processing entity",
  "ModelState": {
    "resource.SourceSymbol": [
      "Source Symbol is required"
    ]
  }
}
```

