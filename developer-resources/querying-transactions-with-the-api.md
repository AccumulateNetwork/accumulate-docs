# Querying transactions with the API

## Getrawtransaction (accumulate query-tx)

After submitting a transaction, the transaction hash in the return can be queried to find the state of the transaction.  There is an optional wait parameter that allows the user to wait for the transaction to fully process and settle before returning.

Request:

```json
{
  "jsonrpc": "2.0",
  "method": "query-tx",
  "params": {
    "txid": "6e2fed60492ad7c5b3588637a2d9a430ab40d5a210fa7e56825b62958060dcbc",
    "wait": {
      "seconds": 10
    }
  },
  "id": 2307
}
```

Response:

```json
{
  "jsonrpc": "2.0",
  "result": {
    "type": "sendTokens",
    "data": {
      "from": "acc://dennyb.acme/acme",
      "to": [
        {
          "url": "acc://5c34c01e38b89a582d817201158aec7ff185353b5a73037f/ACME",
          "amount": "1000000000",
          "txid": "becc54db97fb6cc8bf4e4f320d64988f5a406423e3f404895c14cb1658ad3ae2"
        }
      ]
    },
    "origin": "acc://dennyb.acme/acme",
    "sponsor": "acc://dennyb.acme/acme",
    "transactionHash": "6e2fed60492ad7c5b3588637a2d9a430ab40d5a210fa7e56825b62958060dcbc",
    "txid": "acc://6e2fed60492ad7c5b3588637a2d9a430ab40d5a210fa7e56825b62958060dcbc@dennyb.acme/acme",
    "transaction": {
      "header": {
        "principal": "acc://dennyb.acme/acme",
        "origin": "acc://dennyb.acme/acme",
        "initiator": "2097da5e2ccc78488a1483b194b2695fab8d1f3e87505554cc4e3b595479d1f8"
      },
      "body": {
        "type": "sendTokens",
        "hash": "0000000000000000000000000000000000000000000000000000000000000000",
        "to": [
          {
            "url": "acc://5c34c01e38b89a582d817201158aec7ff185353b5a73037f/ACME",
            "amount": "1000000000"
          }
        ]
      }
    },
    "signatures": [
      {
        "type": "ed25519",
        "publicKey": "de95a9e73655589bb48c585f986810d8435525062eec97a8f52bccced6666dc0",
        "signature": "dc035a21f4302bf7c24701b0f85ac56c14767c33253916384b0d97f840b4f6d0a73a8a162fd441568a08e3d33e30a7006dc9b994a7c090642c4a95e1141c5b04",
        "signer": "acc://dennyb.acme/book/1",
        "signerVersion": 1,
        "timestamp": 1656031727029930,
        "transactionHash": "6e2fed60492ad7c5b3588637a2d9a430ab40d5a210fa7e56825b62958060dcbc"
      }
    ],
    "status": {
      "delivered": true,
      "result": {
        "type": "unknown"
      },
      "initiator": "acc://dennyb.acme/book/1",
      "signers": [
        {
          "type": "keyPage",
          "keyBook": "acc://dennyb.acme/book",
          "url": "acc://dennyb.acme/book/1",
          "acceptThreshold": 1,
          "threshold": 1,
          "version": 1
        }
      ]
    },
    "produced": [
      "acc://becc54db97fb6cc8bf4e4f320d64988f5a406423e3f404895c14cb1658ad3ae2@5c34c01e38b89a582d817201158aec7ff185353b5a73037f/ACME"
    ],
    "syntheticTxids": [
      "acc://becc54db97fb6cc8bf4e4f320d64988f5a406423e3f404895c14cb1658ad3ae2@5c34c01e38b89a582d817201158aec7ff185353b5a73037f/ACME"
    ],
    "signatureBooks": [
      {
        "authority": "acc://dennyb.acme/book",
        "pages": [
          {
            "signer": {
              "type": "keyPage",
              "url": "acc://dennyb.acme/book/1",
              "acceptThreshold": 1
            },
            "signatures": [
              {
                "type": "ed25519",
                "publicKey": "de95a9e73655589bb48c585f986810d8435525062eec97a8f52bccced6666dc0",
                "signature": "dc035a21f4302bf7c24701b0f85ac56c14767c33253916384b0d97f840b4f6d0a73a8a162fd441568a08e3d33e30a7006dc9b994a7c090642c4a95e1141c5b04",
                "signer": "acc://dennyb.acme/book/1",
                "signerVersion": 1,
                "timestamp": 1656031727029930,
                "transactionHash": "6e2fed60492ad7c5b3588637a2d9a430ab40d5a210fa7e56825b62958060dcbc"
              }
            ]
          }
        ]
      }
    ]
  },
  "id": 2307
}
```
