# Table of contents

* [What is AutoShares?](README.md)

## API Documentation

* [Quick Start Guide](web-api/introduction.md)
* [API Overview](web-api/trading-api/overview.md)
* [Authentication](api-documentation/authentication/README.md)
  * [Authenticate with AutoShares SSO/Auth0](api-documentation/authentication/authenticate-with-autoshares-sso-auth0.md)
  * [Triggering authentication with /login](api-documentation/authentication/triggering-authentication-with-login.md)
  * [For logout scenario](api-documentation/authentication/for-logout-scenario.md)
* [Onboarding Users](web-api/trading-api/managing-users/README.md)
  * [Account Setup](web-api/trading-api/managing-users/get-users-info/README.md)
    * [Syntax](web-api/trading-api/managing-users/get-users-info/users\_getuserinfo.md)
    * [Add Account To User](web-api/trading-api/user-accounts/list-users-accounts-6.md)
    * [Add Account To User By Username](web-api/trading-api/user-accounts/list-users-accounts-7.md)
    * [Get All Accounts Of A User](web-api/trading-api/user-accounts/list-users-accounts.md)
    * [Get All Users Of An Account](web-api/trading-api/user-accounts/list-users-accounts-1.md)
    * [Get Account Info](web-api/trading-api/user-accounts/list-users-accounts-2.md)
    * [Update Alias Account For Current User](web-api/trading-api/user-accounts/list-users-accounts-8.md)
    * [Remove Account From User](web-api/trading-api/user-accounts/list-users-accounts-5.md)
    * [Get User's Trading Settings](web-api/trading-api/managing-users/get-users-settings.md)
    * [Get User's Exchanges](web-api/trading-api/managing-users/get-users-exchanges.md)
  * [Access Agreements](web-api/trading-api/agreements/get-a-traders-agreements.md)
* [Account Balances and Buying Power](web-api/trading-api/user-accounts/README.md)
  * [Get Balance Information For A User](web-api/trading-api/managing-users/get-balance-information-for-a-user.md)
  * [Get Account's Balance Info](web-api/trading-api/user-accounts/get-accounts-balance-info.md)
  * [Get Historical Account Value](web-api/trading-api/user-accounts/list-users-accounts-3.md)
* [Order Processing and Trading](web-api/trading-api/orders/README.md)
  * [Place Order](web-api/trading-api/orders/place-order/README.md)
    * [Syntax](web-api/trading-api/orders/place-order/orders\_placeorder.md)
  * [Verify Order Placement](web-api/trading-api/orders/validate-order-placement/README.md)
    * [Syntax](web-api/trading-api/orders/validate-order-placement/orders\_previewcreateorder.md)
  * [Verify Order Replacement](web-api/trading-api/orders/validate-order-replacement/README.md)
    * [Syntax](web-api/trading-api/orders/validate-order-replacement/orders\_previewmodifyorder.md)
  * [Replace Order](web-api/trading-api/orders/replace-order/README.md)
    * [Syntax](web-api/trading-api/orders/replace-order/orders\_replaceorder.md)
  * [Cancel an Order](web-api/trading-api/orders/cancel-order/README.md)
    * [Syntax](web-api/trading-api/orders/cancel-order/orders\_cancelorder.md)
  * [Get Order's Info](web-api/trading-api/orders/get-orders-info/README.md)
    * [Syntax](web-api/trading-api/orders/get-orders-info/orders\_getorder.md)
  * [Get Filtered Orders](web-api/trading-api/orders/get-filtered-orders/README.md)
    * [Syntax](web-api/trading-api/orders/get-filtered-orders/orders\_getorders.md)
  * [Validate Order by ID](web-api/trading-api/orders/validate-order-by-id.md)
  * [Positions](web-api/trading-api/positions/README.md)
    * [Get User's Positions](web-api/trading-api/positions/get-users-positions/README.md)
      * [Syntax](web-api/trading-api/positions/get-users-positions/positions\_getpositions.md)
    * [Get User's Positions in a Security](web-api/trading-api/positions/get-users-positions-in-security/README.md)
      * [Syntax](web-api/trading-api/positions/get-users-positions-in-security/positions\_getpositionbysymbol.md)
    * [Get Market Value of all Security Groups](web-api/trading-api/positions/get-market-value-of-all-security-types.md)
  * [Managing Transactions](web-api/trading-api/managing-transactions/README.md)
    * [Get Transactions](web-api/trading-api/managing-transactions/get-transactions/README.md)
      * [Syntax](web-api/trading-api/managing-transactions/get-transactions/transactions\_getactionspage.md)
* [Streaming Data and Quotes](web-api/trading-api/streaming-data/api-endpoints/README.md)
  * [Streaming API Endpoints](web-api/trading-api/streaming-data/README.md)
    * [Get Streamers' Info](web-api/trading-api/streaming-data/api-endpoints/get-streamers-info.md)
    * [Recover a Streamer Session](web-api/trading-api/streaming-data/api-endpoints/recover-a-streamer-session.md)
  * [Quotes](web-api/trading-api/streaming-data/quotes.md)
  * [Orders](web-api/trading-api/streaming-data/orders.md)
  * [Positions](web-api/trading-api/streaming-data/positions.md)
  * [Watchlists](web-api/trading-api/streaming-data/watchlists.md)
  * [Account Balances](web-api/trading-api/streaming-data/account-balances.md)
  * [User Balance](web-api/trading-api/streaming-data/user-balance.md)
  * [Securities](web-api/trading-api/securities/README.md)
    * [Get Equity Info by Internal ID](web-api/trading-api/securities/get-securitys-info-by-internal-id/README.md)
      * [Syntax](web-api/trading-api/securities/get-securitys-info-by-internal-id/securities\_getequitybyid.md)
    * [Get Equity Info by Ticker](web-api/trading-api/securities/get-securitys-info-by-ticker/README.md)
      * [Syntax](web-api/trading-api/securities/get-securitys-info-by-ticker/securities\_getequitybysymbol.md)
    * [Get Equity Info by Mask](web-api/trading-api/securities/get-securitys-info-by-mask/README.md)
      * [Syntax](web-api/trading-api/securities/get-securitys-info-by-mask/securities\_getequitiesbymask.md)
    * [Get Filtered Equities](web-api/trading-api/securities/get-filtered-equities/README.md)
      * [Syntax](web-api/trading-api/securities/get-filtered-equities/securities\_getequities.md)
    * [Get Option Info by Internal ID](web-api/trading-api/securities/get-option-info-by-internal-id/README.md)
      * [Syntax](web-api/trading-api/securities/get-option-info-by-internal-id/securities\_getoptionbyid.md)
    * [Get Option Info by Ticker](web-api/trading-api/securities/get-option-info-by-ticker/README.md)
      * [Syntax](web-api/trading-api/securities/get-option-info-by-ticker/securities\_getequitybysymbol.md)
    * [Get Options Expiration Dates](web-api/trading-api/securities/get-options-expiration-dates/README.md)
      * [Syntax](web-api/trading-api/securities/get-options-expiration-dates/securities\_getoptionsexpirations.md)
    * [Get an Option Chain](web-api/trading-api/securities/get-an-option-chain.md)
    * [Get Filtered Options](web-api/trading-api/securities/get-filtered-options/README.md)
      * [Syntax](web-api/trading-api/securities/get-filtered-options/securities\_getoptions.md)
    * [Get Company Logo By Symbol](web-api/trading-api/securities/get-company-logo-by-symbol.md)
* [Historical Chart Data](web-api/trading-api/historical-data/README.md)
  * [Get Comparison Chart Data](web-api/trading-api/historical-data/get-chart-data/README.md)
    * [Syntax](web-api/trading-api/historical-data/get-chart-data/historicaltradedata\_getchartcomparedata.md)
  * [Get Candles and Indicators for a Security](web-api/trading-api/historical-data/get-candles-and-indicators-for-charts/README.md)
    * [Syntax](web-api/trading-api/historical-data/get-candles-and-indicators-for-charts/historicaltradedata\_getchartbasicdata.md)
  * [Get Chart Data in the Excel Format](web-api/trading-api/historical-data/get-chart-data-in-the-excel-format/README.md)
    * [Syntax](web-api/trading-api/historical-data/get-chart-data-in-the-excel-format/historicaltradedata\_exporttoexcel.md)
* [Price Alerts](web-api/trading-api/price-alerts/README.md)
  * [Create Price Alert](web-api/trading-api/price-alerts/create-price-alert/README.md)
    * [Syntax](web-api/trading-api/price-alerts/create-price-alert/pricealerts\_createpricealert.md)
  * [Delete Price Alert](web-api/trading-api/price-alerts/delete-price-alert/README.md)
    * [Syntax](web-api/trading-api/price-alerts/delete-price-alert/pricealerts\_deletepricealert.md)
  * [Get Specific Alert](web-api/trading-api/price-alerts/get-specific-alert/README.md)
    * [Syntax](web-api/trading-api/price-alerts/get-specific-alert/pricealerts\_getpricealert.md)
  * [Get User's Price Alerts](web-api/trading-api/price-alerts/get-users-price-alerts/README.md)
    * [Syntax](web-api/trading-api/price-alerts/get-users-price-alerts/pricealerts\_getpricealerts.md)
  * [Modify Price Alert](web-api/trading-api/price-alerts/modify-price-alert/README.md)
    * [Syntax](web-api/trading-api/price-alerts/modify-price-alert/pricealerts\_modifypricealerttrigger.md)
* [Watchlists](web-api/trading-api/watchlists/README.md)
  * [Add Security to Watchlist by ID](web-api/trading-api/watchlists/add-security-to-watchlist-by-id/README.md)
    * [Syntax](web-api/trading-api/watchlists/add-security-to-watchlist-by-id/watchlists\_addsecuritybyid.md)
  * [Add Security to Watchlist by Ticker](web-api/trading-api/watchlists/add-security-to-watchlist-by-ticker/README.md)
    * [Syntax](web-api/trading-api/watchlists/add-security-to-watchlist-by-ticker/syntax.md)
  * [Create New Watchlist](web-api/trading-api/watchlists/create-new-watchlist/README.md)
    * [Syntax](web-api/trading-api/watchlists/create-new-watchlist/watchlists\_createwatchlist.md)
  * [Delete Watchlist](web-api/trading-api/watchlists/delete-watchlist/README.md)
    * [Syntax](web-api/trading-api/watchlists/delete-watchlist/watchlists\_deletewatchlist.md)
  * [Get Specific Watchlist](web-api/trading-api/watchlists/get-specific-watchlist/README.md)
    * [Syntax](web-api/trading-api/watchlists/get-specific-watchlist/watchlists\_getwatchlist.md)
  * [Get User's Watchlists](web-api/trading-api/watchlists/get-users-watchlist/README.md)
    * [Syntax](web-api/trading-api/watchlists/get-users-watchlist/watchlists\_getuserwatchlists.md)
  * [Remove Security From Watchlist by ID](web-api/trading-api/watchlists/remove-security-from-watchlist-by-id/README.md)
    * [Syntax](web-api/trading-api/watchlists/remove-security-from-watchlist-by-id/watchlists\_removesecuritybyid.md)
  * [Remove Security from Watchlist by Ticker](web-api/trading-api/watchlists/remove-security-from-watchlist-by-ticker/README.md)
    * [Syntax](web-api/trading-api/watchlists/remove-security-from-watchlist-by-ticker/watchlists\_removesecurity.md)
  * [Rename Watchlist](web-api/trading-api/watchlists/rename-watchlist/README.md)
    * [Syntax](web-api/trading-api/watchlists/rename-watchlist/watchlists\_editwatchlistname.md)
  * [News](web-api/trading-api/news/README.md)
    * [Get News for a Security](web-api/trading-api/news/get-news-for-a-security.md)
    * [Get Corporate Actions for a Security](web-api/trading-api/news/get-corporate-actions-for-a-security.md)
* [\[Webhooks and SDKs\]](api-documentation/webhooks-and-sdks.md)
* [Wires, ACH, and Account Transfers](web-api/trading-api/account-funding/README.md)
  * [ACH Setup](api-documentation/account-funding/ach-setup/README.md)
    * [Create A New ACH Relationship](web-api/trading-api/account-funding/create-an-ach-relationship.md)
    * [Get an ACH Relationship](web-api/trading-api/account-funding/get-an-ach-relationship.md)
    * [Modify an ACH Relationship](web-api/trading-api/account-funding/modify-an-ach-relationship.md)
  * [Deposit / Withdraw Funds](web-api/trading-api/account-funding/deposit-withdraw-funds-1/README.md)
    * [Deposit / Withdraw Funds via ACH](web-api/trading-api/account-funding/deposit-withdraw-funds-1/deposit-withdraw-funds.md)
  * [Get a Transfer's Info](web-api/trading-api/account-funding/get-a-transfers-info/README.md)
    * [Get an ACH Transfer's Info](web-api/trading-api/account-funding/get-a-transfers-info/get-an-ach-transfers-info.md)
    * [Get All Transfers](web-api/trading-api/account-funding/get-all-transfers.md)
* [Terms and Definitions](web-api/trading-api/definitions/README.md)
  * [Part I](web-api/trading-api/definitions/part-i.md)
  * [Part II](web-api/trading-api/definitions/part-ii.md)
  * [Part III](web-api/trading-api/definitions/part-iii.md)
