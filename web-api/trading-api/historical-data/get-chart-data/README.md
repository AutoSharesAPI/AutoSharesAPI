---
description: Fetch trading data for comparing multiple securities
---

# Get Comparison Chart Data

### Overview

This PUT endpoint enables you to retrieve and compare historical trading data for a set of securities. The data includes price ranges, candles, and various other non-market data. It can be used to draw comparative trading charts as demonstrated by the following screenshot:

![](../../../../.gitbook/assets/screenshot-2019-05-20-at-14.39.46.png)

There are four required parameters that must be provided in the request:

1. **Et-App-Key** (header). This is the unique key of your app that identifies your app when communicating with our service. Contact your administrator to get this key.
2. **Authorization** (header). This is the authorization token from the very first [token request](broken-reference). The value of this header must have the following format: `Bearer BQ898r9fefi` (`Bearer` + 1 space + the token).
3. **API version** (path). Unless necessary, leave it at "1.0".
4. **model** (body). This is a JSON dictionary that contains information about the enquired securities.

#### Enquired Securities Syntax

Here's an example of the request body with the information about the enquired securities.

* Specific period:

```javascript
{"Securities":
    [{"Symbol":"MSFT","Exchange":"XNAS","Currency":"USD","Id":6},
    {"Symbol":"AAPL","Exchange":"XNAS","Currency":"USD","Id":4}],
    "SecuritiesHistorySettings":
    {
        "StartDate":1548046800,
        "EndDate":1550755974,
        "Period":"1h",
    }
}
```

* The last n data points:

```javascript
{"Securities":
    [{"Symbol":"MSFT","Exchange":"XNAS","Currency":"USD","Id":6},
    {"Symbol":"AAPL","Exchange":"XNAS","Currency":"USD","Id":4}],
    "SecuritiesHistorySettings":
    {
        "CandlesCount":10,
        "Period":"1h",
    }
}
```

* The last n data points within a specific time period:

```javascript
{"Securities":
    [{"Symbol":"MSFT","Exchange":"XNAS","Currency":"USD","Id":6},
    {"Symbol":"AAPL","Exchange":"XNAS","Currency":"USD","Id":4}],
    "SecuritiesHistorySettings":
    {
        "CandlesCount":10,
        "Period":"1h",
        "Interval":1,
    }
}
```

where:

| Parameter           | Description                                                                                                                                                                                                                                                                                                         |
| ------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Securities          | This is an array with the enquired securities.                                                                                                                                                                                                                                                                      |
| Symbol              | This is the ticker symbol of the security under which it is listed on the exchange.                                                                                                                                                                                                                                 |
| Exchange (optional) | This is the exchange on which the enquired security is listed.                                                                                                                                                                                                                                                      |
| Currency (optional) | This is the currency in which the enquired security is denominated. Possible values: "USD".                                                                                                                                                                                                                         |
| Id                  | This is the internal ID of the security in AutoShares. You can retrieve this ID with [this API endpoint](../../securities/get-securitys-info-by-internal-id/).                                                                                                                                                      |
| StartDate           | This is the beginning of the period for which the data will be retrieved. The value must be provided in [UNIX Time Stamps](https://www.unixtimestamp.com/).                                                                                                                                                         |
| EndDate             | This is the end of the period for which the data will be retrieved. The value must be provided in [UNIX Time Stamps](https://www.unixtimestamp.com/).                                                                                                                                                               |
| CandlesCount        | This is the number of reference points for the chart. For example, if this parameter is set to 5, that chart will be drawn using five values.                                                                                                                                                                       |
| Period              | <p>This is the preferred time frame for the chart. Possible values:</p><ul><li>"1m";</li><li>"2m";</li><li>"3m";</li><li>"5m";</li><li>"10m";</li><li>"15m";</li><li>"30m";</li><li>"1h";</li><li>"2h";</li><li>"4h";</li><li>"1D";</li><li>"1W";</li><li>"1M";</li><li>"3M";</li><li>"6M";</li><li>"1Y".</li></ul> |
| Interval            | <p>This is the required time period for the specified time period. Possible values:</p><ol><li>"TDY";</li><li>"1D";</li><li>"1W";</li><li>"1M";</li><li>"3M";</li><li>"6M";</li><li>"YTD";</li><li>"1Y";</li><li>"3Y";</li><li>"ALL".</li></ol>                                                                     |

{% hint style="warning" %}
All parameters must be provided in the body JSON; otherwise the chart data will not be retrieved.
{% endhint %}

Here's the final template for this API request:

```
PUT apiURL/v1.0/history/compare
```

### Sample CURLs

```
curl -X PUT --header 'Content-Type: application/json' --header 'Accept: application/json' --header 'Authorization: Bearer token' --header 'Et-App-Key: yourEttAppKey' -d '{"Securities": [{"Symbol":"MSFT","Exchange":"XNAS","Currency":"USD","Id":6},
 {"Symbol":"AAPL","Exchange":"XNAS","Currency":"USD","Id":4}],
 "SecuritiesHistorySettings":
 { "CandlesCount":14,
 "Period":"4h"
 } }' 'https://pub-api-trader-demo-prod.etnasoft.us/api/v1.0/history/compare'
```

### Response

In response to this API request, you'll receive the chart data for the list of specified securities. Notice that trading data for the Microsoft stock comes first, and after it comes the second array with the trading data for the Apple stock.

```javascript
[
  [ //Microsoft data starts
    {
      "Volume": 43020193,
      "Time": 1548028800,
      "Difference": 0,
      "Price": 107.04
    },
    {
      "Volume": 33774774,
      "Time": 1550448000,
      "Difference": 3.66685,
      "Price": 110.965
    }
  ], //Microsoft data ends
  [ //Apple data starts
    {
      "Volume": 97088738,
      "Time": 1548028800,
      "Difference": 0,
      "Price": 157.71
    },
    {
      "Volume": 56357006,
      "Time": 1550448000,
      "Difference": 9.58722,
      "Price": 172.83
    }
  ] //Apple Data ends
]
```

where:

| Parameter  | Description                                                                                   |
| ---------- | --------------------------------------------------------------------------------------------- |
| Volume     | This is the trading volume at the time specified in `Time`.                                   |
| Time       | This is the date and time (in UNIX timestamps) at which this chart data point was registered. |
| Difference | This is the difference between the price at the `StartDate` and `Price`.                      |
| Price      | The price registered at `Time`.                                                               |

### Common Mistakes

Here are some of the common mistakes that developers make when attempting to retrieve trading data for a set of securities.

#### Failing to Specify the Et-App-Key Parameter

If you specify the wrong Et-App-Key parameter or fail to include it in the header altogether, you'll get the following error:

```javascript
{
    "error": "Application key is not defined or does not exist"
}
```

#### Incorrectly Specifying the Request Body

Another common mistake when attempting to retrieve the chart data for a set of securities is incorrectly structuring the request body. It's critical that you follow the template provided above and specify all of the required parameters. Otherwise you'll receive the 500 status code and the following error message:

```javascript
{
    "message": "An error occurred while processing your request",
    "error": "Unexpected server error"
}
```

The following article covers the syntax for this API request in detail.
