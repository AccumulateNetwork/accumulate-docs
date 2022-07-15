# Sending tokens with the API

## sendrawtransaction (accumulate execute-direct / sendTokens)

```json
{
  "jsonrpc": "2.0",
  "method": "execute-direct",
  "params": {
    "envelope": {
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
      "transaction": [
        {
          "header": {
            "principal": "acc://dennyb.acme/acme",
            "initiator": "2097da5e2ccc78488a1483b194b2695fab8d1f3e87505554cc4e3b595479d1f8"
          },
          "body": {
            "type": "sendTokens",
            "to": [
              {
                "url": "acc://5c34c01e38b89a582d817201158aec7ff185353b5a73037f/ACME",
                "amount": "1000000000"
              }
            ]
          }
        }
      ]
    }
  },
  "id": 4013
}

```

Response:

```json
{
  "jsonrpc": "2.0",
  "result": {
    "transactionHash": "6e2fed60492ad7c5b3588637a2d9a430ab40d5a210fa7e56825b62958060dcbc",
    "txid": "acc://6e2fed60492ad7c5b3588637a2d9a430ab40d5a210fa7e56825b62958060dcbc@dennyb.acme/acme",
    "signatureHashes": [
      "8d8ca9288dbd3c3aef0c0ca8d086a220c0f02192fe04bdc576933f547785506d"
    ],
    "simpleHash": "786ba71fe2b07a3b22509c40537f8280479e11a5a47c7cada70106df0b80f293",
    "hash": "786ba71fe2b07a3b22509c40537f8280479e11a5a47c7cada70106df0b80f293",
    "result": {
      "result": {
        "type": "unknown"
      },
      "signers": null
    }
  },
  "id": 4013
}
```
