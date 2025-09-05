```json
{
  "title": "Irys | Querying With GraphQL",
  "url": "https://docs.irys.xyz/build/d/graphql",
  "description": "You can query Irys transaction metadata using GraphQL.",
  "endpoint": "https://uploader.irys.xyz/graphql",
  "queryArguments": [
    {
      "field": "ids",
      "description": "An array of transaction IDs passed as strings. Values are ORed together, matching results will include transactions that have any of the supplied IDs."
    },
    {
      "field": "owner",
      "description": "The address used when posting the transaction. Can be a native address from any of the chains supported by Irys."
    },
    {
      "field": "token",
      "description": "The token used to pay for the transaction."
    },
    {
      "field": "tags",
      "description": "An array of tag name / value pairs passed as JSON objects."
    }
  ],
  "resultsFields": [
    {
      "field": "id",
      "description": "The transaction ID."
    },
    {
      "field": "address",
      "description": "The address used when posting the transaction."
    },
    {
      "field": "token",
      "description": "The token used to pay for the transaction."
    },
    {
      "field": "receipt",
      "description": "An optional receipt, only exists if a user requested one at upload."
    },
    {
      "field": "tags",
      "description": "An array of tags supplied as name / value pairs."
    },
    {
      "field": "timestamp",
      "description": "The timestamp, accurate to the millisecond of when the transaction was posted."
    }
  ],
  "sampleQueries": [
    {
      "query": "query getByIds { transactions(ids: [\"--52WQHJIJod_rni8pkl1Vxt9MFGoXZAm8SC7ex6C1o\", \"--52THRWpX_RJzGcNXmtQ2DSP37d1e1VQ4YmvbY5ZXo\"]) { edges { node { id tags { name value } } } } }",
      "description": "Search by transaction IDs."
    },
    {
      "query": "query getByTimestamp { transactions(timestamp: { from: 1688144401000, to: 1688317201000 }) { edges { node { id } } } }",
      "description": "Search by timestamps."
    }
  ],
  "metadata": {
    "favicon": "https://docs.irys.xyz/favicon.ico",
    "ogImage": "https://docs.irys.xyz/opengraph-image.png?8c892bc9b92ee1a8",
    "language": "en"
  }
}
```