---
description: Withdraw funds via checks
---

# Withdraw Funds via Checks

### Introduction <a href="#withdrawing-funds-with-checks" id="withdrawing-funds-with-checks"></a>

This POST endpoint enables you to withdraw funds from your trading account by means of a check.&#x20;

In addition to ACH transfers, AutoShares also enables traders to withdraw funds from their trading account by means of a check. In this case a check with the specified sum will be sent to the address specified by the trader in the account opening form (the one you filled out when opening the trading account).

{% hint style="warning" %}
Check transfers are available only for withdrawing funds.
{% endhint %}

There are five required parameters that must be provided in the request:

1. **Et-App-Key** (header). This is the unique key of your app that identifies your app when communicating with our service. Contact your administrator to get this key.
2. **Authorization** (header). This is the authorization token from the very first [token request](../../authentication/). The value of this header must have the following format: `Bearer BQ898r9fefi` (`Bearer` + 1 space + the token).
3. **API version** (path). Unless necessary, leave it at "1.0".
4. **accountId** (path). This is the [internal identifier](../../user-accounts/list-users-accounts.md) of the trading account in AutoShares.
5. **model** (body). This is a JSON file containing detailed information about the check withdrawal.

#### Body Syntax

The body of the request represents a JSON file containing all required parameters for performing a funds transfer.

| Parameter      | Required | Description                                                                                                                                                                 |
| -------------- | -------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Amount         | True     | This is the amount of funds to be withdrawn. The value must be provided in US dollars. Set this parameter to `null` if `CloseAccount` is set to `true`.                     |
| CloseAccount   | True     | This boolean value indicates if the trading account must be closed after the withdrawal is performed.                                                                       |
| Memos          | False    | An associated comment. Must be provided as an array containing one value.                                                                                                   |
| DeliveryMethod | True     | <p>The preferred check delivery method. Possible values:</p><ul><li>STANDARD</li><li>OVERNIGHT</li><li>SATURDAY</li><li>OVERNIGHT_TO_BROKER</li><li>PRINT_AT_FIRM</li></ul> |

For example:

{% tabs %}
{% tab title="Partial Withdrawal" %}
```javascript
{
    "Amount":100,
    "CloseAccount":false,
    "Memos":[],
    "DeliveryMethod":"STANDARD"
}
```
{% endtab %}

{% tab title="Complete Withdrawal" %}
```javascript
{
    "Amount":null,
    "CloseAccount":true,
    "Memos":["Test comment"],
    "DeliveryMethod":"STANDARD"
}
```
{% endtab %}
{% endtabs %}

Here's the final template for this API request:

```
POST apiURL/v1.0/accounts/{accountId}/transfers/check
```

### Response

In response to this API request, you will receive a JSON dictionary containing detailed information about the withdrawal:

```javascript
{
    "Id":"ec20773e-d659-404a-b102-08d8dcc6185a",
    "AccountId":0,
    "Mechanism":"Check",
    "IsDeposit":false,
    "Status":"Submitted",
    "Amount":0.0,
    "TotalAmount":0.0,
    "CreatedAt":"2021-03-01T15:40:25.4533333Z",
    "ClearingAccountNumber":"5DP05506"
}
```

### Common Mistakes

Here are some of the common mistakes that developers make when attempting to send a request to withdraw funds via checks.

#### Failing to Specify the Et-App-Key Parameter

If you specify the wrong Et-App-Key parameter or fail to include it in the header altogether, you'll get the following error:

```javascript
{
    "error": "Application key is not defined or does not exist"
}
```
