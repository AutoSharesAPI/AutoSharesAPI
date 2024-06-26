---
description: Get a user's information by their AutoShares identifier
---

# Account Setup

## Overview

This endpoint enables you to request a user's information by supplying their unique AutoShares identifier in the header. In response, you'll receive a JSON file with the user's information.

There are few required parameters that must be provided in the request:



1. **Authorization** (header). This is the authorization token from the very first token request. The value of this header must have the following format: `Bearer BQ898r9fefi` (`Bearer` + 1 space + the token).
2. **Internal user ID** (path). This is the numeric ID of the user whose information you'd like to receive.
3. **API version** (path). Unless necessary, leave it at "1.0"

The user information request must be sent to the following URL:

```
apiURL/v1.0/users/644(userID)/info
```

## Response

In response, you'll receive a JSON file with the information about this user:

```javascript
{
    "UserId": 644, //this is the ID from the path
    "FirstName": "Robert",
    "MiddleName": "",
    "LastName": "Zakiev",
    "Login": "robert.zak",
    "Email": "someEmail@etnatrader.com",
    "AddedDate": "2019-01-14T12:27:37.6205663Z",
    "Salutation": "NoSalutation",
    "Suffix": "NoSuffix"
}
```

where:

| Parameter  | Description                                                                 |
| ---------- | --------------------------------------------------------------------------- |
| UserId     | This is the internal ID of the user in AutoShares.                          |
| FirstName  | This is the first name of the user.                                         |
| MiddleName | This is the middle name of the user.                                        |
| LastName   | This is the last name of the user.                                          |
| Login      | This is the user's login in AutoShares.                                     |
| Email      | This is the email address of the user in AutoShares.                        |
| AddedDate  | This is the date on which this user account was added to AutoShares.        |
| Salutation | This is a special salutation used to address this user in emails.           |
| Suffix     | This is the suffix used when addressing the user (Jr, Sr, I, II, III, etc.) |

## Common Mistakes

Here are some of the common mistakes that developers make when requesting a user's information:

###

### Specifying a Non-Existent User ID Instead of the Internal One

Another common mistake when making this request is specifying a non-existent user ID. Doing so will result in the 500 status code and the following error message:

```javascript
{
  "Model": null,
  "Errors": [
    "Value cannot be null.\r\nParameter name: user"
  ],
  "StatusCode": 500,
  "IsSucceed": false
}
```

In the following article we provide in-depth coverage of the syntax for this API request.
