```json
{
  "title": "Irys | Account API",
  "url": "https://docs.irys.xyz/build/d/rest-api/account",
  "description": "These routes query the Irys Labs bundler for account details, such as retrieving account balances.",
  "routes": [
    {
      "method": "GET",
      "path": "/account/balance/{token}",
      "description": "Get user balance for token",
      "operationId": "get_account_balance__token_"
    },
    {
      "method": "GET",
      "path": "/account/approval",
      "description": "Get approval information",
      "operationId": "get_account_approval"
    },
    {
      "method": "POST",
      "path": "/account/withdraw",
      "description": "Withdraw user balance",
      "operationId": "post_account_withdraw"
    },
    {
      "method": "GET",
      "path": "/account/withdrawals/{token}",
      "description": "Get withdrawals for token",
      "operationId": "get_account_withdrawals__token_"
    },
    {
      "method": "GET",
      "path": "/account/withdrawals",
      "description": "Get all withdrawals",
      "operationId": "get_account_withdrawals"
    }
  ],
  "metadata": {
    "og:title": "Irys | Account API",
    "og:image": "https://docs.irys.xyz/opengraph-image.png?8c892bc9b92ee1a8",
    "twitter:card": "summary_large_image",
    "language": "en",
    "favicon": "https://docs.irys.xyz/favicon.ico"
  }
}
```