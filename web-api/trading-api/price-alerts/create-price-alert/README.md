---
description: Create a new price alert
---

# Create Price Alert

## Overview

This POST endpoint enables you to create a new price alert for the user whose ID is provided in the request's body. Price alerts are essentially notifications that are sent to the user when the alert's conditions are satisfied by the market. For example, a user may have a price alert that will notify them when the price of the Apple stock exceeds $200.

There are five required parameters that must be provided in the request:

1. **Authorization** (header). This is the authorization token from the very first [token request](broken-reference). The value of this header must have the following format: `Bearer BQ898r9fefi` (`Bearer` + 1 space + the token).
2. **API version** (path). Unless necessary, leave it at "1.0".
3. **userID** (path). This is the ID of the user to whose account a new price alert should be added.
4. **model** (body). This is a JSON dictionary that contains information about the new price alert.

### Body Syntax

Here's an example of the request body with the information about the new price alert:

```javascript
{
    "State": "New",
    "Operator": "GTEQ",
    "SecurityId": 4,
    "Field": "Bid",
    "Argument": 200,
    "ExpirationDate": 1550674384
}
```

{% hint style="warning" %}
All six parameters must be indicated in the body JSON; otherwise the price alerts will be improperly interpreted by the system.
{% endhint %}

Here's the final template for this API request:

```
POST apiURL/v1.0/users/{userID}/pricealerts
```

## Response

In response to this API request, you'll receive a JSON file with a more detailed information about the newly created price alert.

```javascript
{
    "Id": 871,
    "State": "New",
    "CreatedDate": 1550588008,
    "Operator": "GTEQ",
    "SecurityId": 2829,
    "Field": "Bid",
    "Argument": 170,
    "ExpirationDate": 1550674384
}
```

where:

| Parameter      | Description                                                                                                          |
| -------------- | -------------------------------------------------------------------------------------------------------------------- |
| Id             | This is the internal identifier of the price alert.                                                                  |
| State          | This is the state of the price alert. Possible values: New, Expired, Completed, Stopped.                             |
| CreatedDate    | This is the date on which the price alert was created (in ticks).                                                    |
| Operator       | This is the condition of the price alert. Possible values: GTEQ (greater or equal to), LTEQ (less than or equal to). |
| SecurityId     | This is the ID of the security for which the price alert is configured.                                              |
| Field          | This is the referent price for the price alert. Possible values: Ask, Bid, Last.                                     |
| Argument       | This is the price point at which the price alert will be triggered and the user will be notified.                    |
| ExpirationDate | This is the expiration date of the price alert (in ticks).                                                           |

## Common Mistakes

Here are some of the common mistakes that developers make when attempting to create a new price alert.

The following article covers the syntax for this API request in detail.
