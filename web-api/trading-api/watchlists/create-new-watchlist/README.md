---
description: Create a new watchlist for a particular user
---

# Create New Watchlist

## Overview

This POST endpoint enables you to create a new watchlist for a user whose internal ID is provided in the request's path. The newly created watchlist can initially have either no securities or it could have a list of initial securities provided as an array.

There are six required parameters that must be provided in the request:

1. **Authorization** (header). This is the authorization token from the very first [token request](broken-reference). The value of this header must have the following format: `Bearer BQ898r9fefi` (`Bearer` + 1 space + the token).
2. **API version** (path). Unless necessary, leave it at "1.0".
3. **userID** (path). This is the ID of the user for whom a new watchlist will be created.
4. **resultIncludeSecurities** (query). This field indicates if the retrieved watchlist should include its corresponding stocks.
5. **watchlist** (body). This is the new watchlist.

### New Watchlist Template

All new watchlists must be of the _**application/json**_ content type. The syntax for new watchlists is as follows:

### Empty Watchlist Sample

{% code title="New Watchlist Template" %}
```javascript
{
    "Name": "Nifty Fifty" 
}
```
{% endcode %}

### A Comprehensive Watchlist Sample

```javascript
{
    "Name": "Apple & Google" ,
    "Securities": [4,5] //internal ID of the securities in the new watchlist
}
```

Internal ID of the required securities can be fetched using [this API request](../../securities/get-securitys-info-by-ticker/).

Here's the final template for this API request:

```
POST apiURL/v1.0/users/{userID}/watchlists/?resultIncludeSecurities=true
```

## Response

In response to this API request, you'll receive a JSON file with the information about the newly created watchlist. If the _**resultIncludeSecurities**_ is set to true, the response will contain the securities in this watchlist.

```javascript
{
  "Id": 19302,
  "Name": "Apple & Google",
  "Type": "UserList",
  "CreateDate": "2019-02-15T18:15:01.7237322Z",
  "ModifyDate": "2019-02-15T18:15:01.7237322Z",
  "ReadOnly": false,
  "SecurityList": [
    {
      "Id": 4,
      "Symbol": "AAPL",
      "Description": "Apple Inc.",
      "Exchange": "XNAS",
      "Currency": "USD",
      "AddedDate": "2012-11-29T16:05:43.993Z",
      "ModifyDate": "2018-12-10T08:00:22.2867686Z",
      "Type": "CommonStock",
      "Source": 0,
      "ParentId": -1,
      "OptionType": "Undefined",
      "ExpirationType": "Undefined",
      "ExpirationDate": "0001-01-01T00:00:00Z",
      "StrikePrice": 0,
      "SeriesId": -1,
      "ContractSize": 1,
      "Precision": 2,
      "VolumePrecision": 0,
      "TickSize": 0.01,
      "MarginRate": 0
    },
    {
      "Id": 5,
      "Symbol": "GOOG",
      "Description": "Alphabet Inc.",
      "Exchange": "XNAS",
      "Currency": "USD",
      "AddedDate": "2012-11-29T16:05:43.993Z",
      "ModifyDate": "2017-12-14T08:00:10.1826129Z",
      "Type": "CommonStock",
      "Source": 0,
      "ParentId": -1,
      "OptionType": "Undefined",
      "ExpirationType": "Undefined",
      "ExpirationDate": "0001-01-01T00:00:00Z",
      "StrikePrice": 0,
      "SeriesId": -1,
      "ContractSize": 1,
      "Precision": 2,
      "VolumePrecision": 0,
      "TickSize": 0.01,
      "MarginRate": 0
    }
  ]
}
```

where:

| Parameter    | Description                                                                                                                   |
| ------------ | ----------------------------------------------------------------------------------------------------------------------------- |
| Id           | This is the internal identifier of the watchlist in AutoShares.                                                               |
| Name         | This is the name of the watchlist in AutoShares.                                                                              |
| Type         | This is the type of the watchlist. It could either be a user-created watchlist or a default watchlist provided by the system. |
| CreateDate   | This is the date on which the watchlist was created.                                                                          |
| ModifyDate   | This is the date on which the watchlist was last modified.                                                                    |
| ReadOnly     | This field indicates if the watchlist is modifiable.                                                                          |
| SecurityList | This is a collection of securities in the watchlist.                                                                          |

## Common Mistakes

Here are some of the common mistakes that developers make when attempting to create a new watchlist.

### Sending Improperly Constructed Watchlist

It's critical that you precisely follow the watchlist template at the beginning of this page and properly prepare the JSON with the new watchlist. Improperly specifying certain fields will lead to the 409 status code:

```javascript
{
    "NameZZZ": "Apple & Google" , //incorrect first parameter
    "Securities": [4,5] //internal ID of the securities in the new watchlist
}
```

The following article covers the syntax for this API request in detail.
