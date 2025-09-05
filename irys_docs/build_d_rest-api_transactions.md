```json
{
  "date": "2025-09-03T09:14:33.888Z",
  "title": "Irys | Transaction API",
  "url": "https://docs.irys.xyz/build/d/rest-api/transactions",
  "description": "These routes post new transactions to the Irys Labs bundler and also query the bundler for information about transactions.",
  "routes": [
    {
      "method": "POST",
      "path": "/tx",
      "description": "Post transaction",
      "operationId": "post_tx"
    },
    {
      "method": "POST",
      "path": "/tx/{token}",
      "description": "Post transaction",
      "operationId": "post_tx__token_"
    },
    {
      "method": "HEAD",
      "path": "/tx/{txId}/data",
      "description": "Get transaction data",
      "operationId": "head_tx__txId__data"
    },
    {
      "method": "GET",
      "path": "/tx/{txId}/data",
      "description": "Get transaction data",
      "operationId": "get_tx__txId__data"
    },
    {
      "method": "GET",
      "path": "/tx/{txId}/status",
      "description": "Get transaction status",
      "operationId": "get_tx__txId__status"
    },
    {
      "method": "GET",
      "path": "/tx/{txId}/tags",
      "description": "Get transaction tags",
      "operationId": "get_tx__txId__tags"
    },
    {
      "method": "GET",
      "path": "/tx/{txId}",
      "description": "Get transaction metadata",
      "operationId": "get_tx__txId_"
    }
  ],
  "metadata": {
    "twitter": {
      "card": "summary_large_image",
      "title": "Irys | Transaction API",
      "image": {
        "url": "https://docs.irys.xyz/opengraph-image.png?8c892bc9b92ee1a8",
        "width": 1200,
        "height": 600
      }
    },
    "og": {
      "title": "Irys | Transaction API",
      "image": {
        "url": "https://docs.irys.xyz/opengraph-image.png?8c892bc9b92ee1a8",
        "width": 1200,
        "height": 600
      }
    },
    "favicon": "https://docs.irys.xyz/favicon.ico",
    "language": "en",
    "statusCode": 200,
    "contentType": "text/html; charset=utf-8",
    "sourceURL": "https://docs.irys.xyz/build/d/rest-api/transactions"
  }
}
```