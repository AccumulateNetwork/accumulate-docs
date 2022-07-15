# Send a transaction with the API

### Getting the balance of a token account

Accumulate maintains the current state of all accounts. So querying an account you receive the current state. Therefore, you can query the account for current balance along with a receipt that you can use to prove the balance is authentic and current. Token accounts take 2 forms:

*   A Lite account, where you have 1 private key that manages an account similar to a bitcoin or Ethereum private key controlling the btc or eth address.


* An ADI token account, where you have a token account part of a user’s Accumulate Digital Identifier domain. You can think of an ADI as an analogy to an traditional internet domain, e.g. “example.com.” The owner of an ADI can have sub accounts within it, for example, acc://dennyb.acme/acmetokens, where “acmetokens” is designated as the ACME token account.

### _Query a user’s token account_

For this example, the user’s domain (ADI) is dennyb.acme with a token account “acme,” so the user’s token account URL is acc://dennyb.acme/acme. We also want to “prove” the validity of the balance state, so we also include “prove” true parameter.

Example Query:

```json
{
  "jsonrpc": "2.0",
  "method": "query",
  "params": {
    "url": "acc://dennyb.acme/acme",
    "prove": true
  },
  "id": 2886
}
```

Example Response:

```json
{
  "jsonrpc": "2.0",
  "result": {
    "type": "tokenAccount",
    "mainChain": {
      "height": 2,
      "count": 2,
      "roots": [
        null,
        "f9e6669db704564739e602b7bfb5cec3f256fa3ed77889c2bb43a104e138206e"
      ]
    },
    "merkleState": {
      "height": 2,
      "count": 2,
      "roots": [
        null,
        "f9e6669db704564739e602b7bfb5cec3f256fa3ed77889c2bb43a104e138206e"
      ]
    },
    "chains": [
      {
        "name": "main",
        "type": "transaction",
        "height": 2,
        "count": 2,
        "roots": [
          null,
          "f9e6669db704564739e602b7bfb5cec3f256fa3ed77889c2bb43a104e138206e"
        ]
      },
      {
        "name": "minor-main-index",
        "type": "index",
        "height": 2,
        "count": 2,
        "roots": [
          null,
          "4e15b8e049e4395ab0dee230984dcd66894113c5025fd6811faaba33440ba9b4"
        ]
      }
    ],
    "data": {
      "type": "tokenAccount",
      "keyBook": "acc://dennyb.acme/book",
      "url": "acc://dennyb.acme/acme",
      "authorities": [
        {
          "url": "acc://dennyb.acme/book"
        }
      ],
      "tokenUrl": "acc://acme",
      "balance": "100000000000"
    },
    "chainId": "68d2f226c65c3167b6ee03d955a502163e0aa6dc5adba44aa6842283cd698ea1",
    "receipt": {
      "localBlock": 2083,
      "proof": {
        "start": "14eb1c0347f08be1aebf0685c8b34c05a3684478d7b7ff586322e379acdd4705",
        "endIndex": 2,
        "anchor": "1887d029f85f05dab9a2a36f3799d88e910675c273ad5cdb8089b2c020295100",
        "entries": [
          {
            "right": true,
            "hash": "5b39602110b09eb4677c60f666f2cf223551efaaa6254f379dbc71d7ac9f661b"
          },
          {
            "right": true,
            "hash": "0000000000000000000000000000000000000000000000000000000000000000"
          },
          {
            "right": true,
            "hash": "ad3e10da0483b25754c4bbeaa12bd1c8d1a3f56af03fbaf3b92637cb9c872d43"
          },
          {
            "hash": "75bbe4596498d3d247eefe0e05a33e5cb54e937fd5ca72255790a31ec1f862f9"
          },
          {
            "right": true,
            "hash": "dfea9efff9d2c4b1316b64344c24051cef9a481ad0c8a00089d39ab19ceb8cf9"
          },
          {
            "hash": "3592319586fb04d75d57311e30803197c4e9f819d7c4239daf324e78042ae8a8"
          },
          {
            "hash": "e4dd326dedf993814a6d8bf11056272472231ee15a13a652950533a07022f359"
          }
        ]
      }
    }
  },
  "id": 2886
}
```

In the response there is a lot of information, however, the key things to note are 1) the data parameter, and 2) the receipt.

### The data parameter

The data field contains the details of the account state. Because “acc://dennyb.acme/acme” is configured as an acme token account, it will show the token account state information, which includes the token balance, token type, and controlling key authorities of the account.

```json
"data": {
      "type": "tokenAccount",
      "keyBook": "acc://dennyb.acme/book",
      "url": "acc://dennyb.acme/acme",
      "authorities": [
        {
          "url": "acc://dennyb.acme/book"
        }
      ],
      "tokenUrl": "acc://acme",
      "balance": "100000000000"
    },
```

The parameters of the token are broken down in the following table:



| Parameter   | Value                  | Description                                                                                                                                                                         |
| ----------- | ---------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| type        | tokenAccount           | Specifies the type of account this is. If you are only interested in tokens, then the types will be “tokenAccount” or “liteTokenAccount”                                            |
| keyBook     | acc://dennyb.acme/book | This is the url in the adi that manages the authroized keys                                                                                                                         |
| url         | acc://dennyb.acme/acme | Url of this account                                                                                                                                                                 |
| authorities | acc://dennyb.acme/book | The list of key books authorized to manage the account                                                                                                                              |
| tokenUrl    | acc://acme             | identifies what type of account this is, which for ACME tokens is the URL acc://acme                                                                                                |
| balance     | 100000000000           | The acc://acme account contains the parameters of the token, which include the precision, which for acme is 8 decimal places.  So this balance represents 1000.00000000 acme tokens |

### The receipt parameter

The receipt field contains the details needed to prove the state is genuine against a separate anchor. The general concept is the anchor is published by the directory node at predetermined intervals. These anchors contain the status of the entire state of the network up to that point. Given an anchor, one can prove the state of the account is valid by executing an algorithms over the receipt. There is currently no endpoint api to facilitate this, so implementation is left up to the user. An example use case for this and implementation detail is outlined here.

{% embed url="https://gitlab.com/accumulatenetwork/sdk/anchor-solidity" %}
