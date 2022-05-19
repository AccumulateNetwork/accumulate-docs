# API Reference

Clients interact with Accumulate through APIs calls to nodes.

For guidance on how to issue API calls, please see [Issuing API Calls](broken-reference).

For a list of API calls and their parameters, please see [API Reference](broken-reference).



### Endpoint

API calls are made to a node endpoint, which is a URL. The base URL follows this format:

* `[node-ip]` is the IP address for the node you are connecting to.
* `[http-port]` is the port that the node you are connecting to is listening for HTTP calls.
* All API calls are made to the `/v2` endpoint.

By default, the API is exposed on port 26660, so the node URL will be `<hostname>:26660/v2`.

#### Public API Testnet Endpoint

There is a Public Testnet JSON-RPC API server (18.119.26.7) that allows developers to access the Accumulate Testnet network without having to run a node themselves.

The public API server is at `https://testnet.accumulatenetwork.io/v2` for Accumulate Testnet.

### JSON RPC Formatted APIs

The Accumulate API uses the [OpenRPC](https://open-rpc.org/) specification for JSON-RPC 2.0 to describe its requests and responses.

#### Example Request

Let's say you want to retrieve the Public Key of an ADI (Accumulate Digital Identifier). You would call the `adi` method to retrieve this information.

The endpoint we send our API call to is always`[node-ip]:[http-port]/v2`

The required parameter for the `adi` request is `url`, which is the Accumulate ADI URL that you are requesting information on.

To call this method, you would send a request as such:

```d
curl -X POST --data '{
    "jsonrpc": "2.0",
    "id": 0,
    "method": "adi",
    "params": {
        "url": "acc://RedWagon"
    }
}' -H 'content-type:application/json;' 127.0.0.1:9650/v1
```

* `jsonrpc` is the version of the JSON-RPC protocol this API uses (always 2.0).
* `method` specifies the method you want to call.
* `params` specifies the parameters for this method.
* `id` is the ID of this request. This is chosen by the sender.

#### Example Response

If you run the above call, you should receive a response as such:

```d
{
    "jsonrpc": "2.0",
    "result": {
        "url": "acc://RedWagon",
        "publicKeyHash": "acc2ed111975d438e64bd2eb455be285b186e5ebd525d45dd8c274dff30edb59",
    },
    "id": 0
}
```

####

#### Example Error

Sometimes in life things go wrong, and you can't figure out why. In this case however, you'll get an error message.

For our `adi` request, the `url` we passed might not exist. If that's the case, you'll receive an error message like such:

```d
{
    "jsonrpc": "2.0",
    "error": {
        "code": -32902,
        "message": "adi does not exist",
        "data": "some extra data about this error"
    },
    "id": 1
}
```







### Format

This API uses the JSON-RPC 2.0 format. For more information on making JSON-RPC calls, see [Issuing API Calls](broken-reference).

### Endpoint

`[node-ip]:[http-port]/v2`

#### Testnet Endpoint

`https://testnet.accumulatenetwork.io/v2`

## Methods : Query methods

### query

Returns Accumulate Object by URL

**Request Parameters**

| Parameter | Type   | Description        | Required? |
| --------- | ------ | ------------------ | --------- |
| `url`     | string | Any Accumulate URL | Yes       |

**Response Properties**

| Property      | Type   | Description                                |
| ------------- | ------ | ------------------------------------------ |
| `type`        | string | The Accumulate object type                 |
| `merkleState` | object | The merkle-state for this object           |
| `data`        | object | The data for this object (properties vary) |

**Example Request**

```cpp
curl -X POST --data '{
    "jsonrpc": "2.0",
    "id": 0,
    "method": "query",
    "params": {
        "url": "acc://5fd54e898c2c60e9757d2cd36f3a14b6df895b237690afb1/ACME"
    }
}' -H 'content-type:application/json;' https://testnet.accumulatenetwork.io/v2
```

**Example Response**

```d
{
    "jsonrpc": "2.0",
    "result": {
        "type": "liteTokenAccount",
        "merkleState": {
            "count": 1,
            "roots": [
                "c7e59bfea5029963ee07c27a09e5e7467e30cd4ebc1822e16ebbb173a8ff685c"
            ]
        },
        "data": {
            "type": "liteTokenAccount",
            "url": "acc://5fd54e898c2c60e9757d2cd36f3a14b6df895b237690afb1/ACME",
            "keyBook": "0000000000000000000000000000000000000000000000000000000000000000",
            "managerKeyBook": "",
            "tokenUrl": "acc://ACME",
            "balance": 1000000000,
            "txCount": 1,
            "creditBalance": 0
        }
    },
    "id": 0
}
```

**Example Request**

```cpp
curl -X POST --data '{
    "jsonrpc": "2.0",
    "id": 0,
    "method": "query",
    "params": {
        "url": "adione"
    }
}' -H 'content-type:application/json;' https://testnet.accumulatenetwork.io/v2
```

**Example Response**

```d
{
    "jsonrpc": "2.0",
    "result": {
        "type": "identity",
        "merkleState": {
            "count": 1,
            "roots": [
                "beddcee7767ee7ca2f717b5ae6d993e373aaa0ccb5957fcefb78c03f43838139"
            ]
        },
        "data": {
            "type": "identity",
            "url": "acc://adione",
            "keyBook": "a305417c7e8e46fd3f7da558f2836693f1e554697f5207e4d48881dcb7baea0c",
            "managerKeyBook": "",
            "keyType": "sha256",
            "keyData": "40e1bc668a0ddb6ef0f80ecf0cb4f8090b87e78de29a3b177b98ea21a7683a66",
            "nonce": 2
        }
    },
    "id": 0
}
```

### query-tx-history

Returns account history for the specified token account

**Request Parameters**

| Parameter | Type   | Description                   | Required? |
| --------- | ------ | ----------------------------- | --------- |
| `url`     | string | Token Account URL             | Yes       |
| `count`   | int    | Count of history transactions | Yes       |

**Response Properties**

| Property          | Type   | Description                                |
| ----------------- | ------ | ------------------------------------------ |
| `type`            | string | The Accumulate object type                 |
| `data`            | object | The data for this object (properties vary) |
| `sponsor`         | string | The data for this object (properties vary) |
| `keypage`         | object | The Keypage for this object                |
| `txid`            | string | Transaction id                             |
| `transactionHash` | string | Transaction hash                           |
| `signatures`      | object | ADI signing the creation of new token      |
| `status`          | object | Status                                     |

**Example Request**

```cpp
curl -X POST --data '{
    "jsonrpc": "2.0",
    "id": 0,
    "method": "query-tx-history",
    "params": {
        "url": "acc://5fd54e898c2c60e9757d2cd36f3a14b6df895b237690afb1/ACME",
        "count": 1
    }
}' -H 'content-type:application/json;' https://testnet.accumulatenetwork.io/v2
```

**Example Response**

```d
{
    "jsonrpc": "2.0",
    "result": {
        "type": "txHistory",
        "items": [
            {
                "type": "syntheticDepositTokens",
                "data": {
                    "cause": "395caba8d27056614abf991ab40a1b53a8b8babc4919d34ababa24f603f8a1a3",
                    "token": "ACME",
                    "amount": "1000000000"
                },
                "origin": "acc://09bca3fcd7e28434f4fb5a3c7317d64e955acbc102e45df5/ACME",
                "sponsor": "acc://09bca3fcd7e28434f4fb5a3c7317d64e955acbc102e45df5/ACME",
                "keyPage": {
                    "height": 1,
                    "index": 0
                },
                "transactionHash": "2bd403d477d70b87e35e88b0aa316242d89aa41db5b5dea6df5a1c470e424671",
                "txid": "2bd403d477d70b87e35e88b0aa316242d89aa41db5b5dea6df5a1c470e424671",
                "signatures": [
                    {
                        "Nonce": 390,
                        "PublicKey": "Kdjx5D4pOOIrd/gNV3S+21DF5g93dR6IZ1ZfwfDi94g=",
                        "Signature": "tyKHXcPWzJBwkNJOTljvYmRQdzi9eJROgfIVJkcIJ6+HnmrYZnTtCKz5jE/Q5mKfvqiquAfEvUWw4nXHjpEMAA=="
                    }
                ],
                "status": {
                    "delivered": true,
                    "result": {}
                }
            },
            {
                "type": "syntheticDepositTokens",
                "data": {
                    "cause": "4d253e95399ccbd6b7044d1fff85a6a7d6dd83ab209cdd25a416dd2c70c21e9d",
                    "token": "ACME",
                    "amount": "1000000000"
                },
                "origin": "acc://09bca3fcd7e28434f4fb5a3c7317d64e955acbc102e45df5/ACME",
                "sponsor": "acc://09bca3fcd7e28434f4fb5a3c7317d64e955acbc102e45df5/ACME",
                "keyPage": {
                    "height": 1,
                    "index": 0
                },
                "transactionHash": "bc573897d25828887b393a54ba8378d6af20298738dc909af4fb86c553689c9c",
                "txid": "bc573897d25828887b393a54ba8378d6af20298738dc909af4fb86c553689c9c",
                "signatures": [
                    {
                        "Nonce": 516,
                        "PublicKey": "Kdjx5D4pOOIrd/gNV3S+21DF5g93dR6IZ1ZfwfDi94g=",
                        "Signature": "y02cNToZnoqabkIY8V2v3UjQvdh47JNQzjlFHpsdYVsFQUtYIWZDJKzS8nahTcTfdoPH0SR4dEZ373W+AeAiAQ=="
                    }
                ],
                "status": {
                    "delivered": true,
                    "result": {}
                }
            }
        ],
        "start": 0,
        "count": 2,
        "total": 40
    },
    "id": 0
}
```

### query-tx

Returns transaction data for the specified transaction

**Request Parameters**

| Parameter | Type   | Description      | Required? |
| --------- | ------ | ---------------- | --------- |
| `txid`    | string | Transaction hash | Yes       |

**Response Properties**

| Property          | Type   | Description                                |
| ----------------- | ------ | ------------------------------------------ |
| `type`            | string | The Accumulate object type                 |
| `data`            | object | The data for this object (properties vary) |
| `sponsor`         | string | The data for this object (properties vary) |
| `keypage`         | object | The Keypage for this object                |
| `txid`            | string | Transaction hash                           |
| `transactionHash` | string | Transaction hash                           |
| `signatures`      | object | ADI signing the creation of new token      |
| `status`          | object | Status                                     |

**Example Request**

```cpp
curl -X POST --data '{
    "jsonrpc": "2.0",
    "id": 0,
    "method": "query-tx",
    "params": {
        "txid": "9dce91ec75f5b5e767283d8db77394daeef6e50b4f0e1197624f1a888ed076b1"
    }
}' -H 'content-type:application/json;' https://testnet.accumulatenetwork.io/v2
```

**Example Response**

```d
{
    "jsonrpc": "2.0",
    "result": {
        "type": "syntheticDepositTokens",
        "data": {
            "cause": "395caba8d27056614abf991ab40a1b53a8b8babc4919d34ababa24f603f8a1a3",
            "token": "ACME",
            "amount": "1000000000"
        },
        "origin": "acc://09bca3fcd7e28434f4fb5a3c7317d64e955acbc102e45df5/ACME",
        "sponsor": "acc://09bca3fcd7e28434f4fb5a3c7317d64e955acbc102e45df5/ACME",
        "keyPage": {
            "height": 1,
            "index": 0
        },
        "transactionHash": "2bd403d477d70b87e35e88b0aa316242d89aa41db5b5dea6df5a1c470e424671",
        "txid": "2bd403d477d70b87e35e88b0aa316242d89aa41db5b5dea6df5a1c470e424671",
        "signatures": [
            {
                "Nonce": 390,
                "PublicKey": "Kdjx5D4pOOIrd/gNV3S+21DF5g93dR6IZ1ZfwfDi94g=",
                "Signature": "tyKHXcPWzJBwkNJOTljvYmRQdzi9eJROgfIVJkcIJ6+HnmrYZnTtCKz5jE/Q5mKfvqiquAfEvUWw4nXHjpEMAA=="
            }
        ],
        "status": {
            "delivered": true,
            "result": {}
        }
    },
    "id": 0
}
```

### query-chain

Get query-chain properties

**Request Parameters**

| Parameter | Type   | Description | Required? |
| --------- | ------ | ----------- | --------- |
| `chainId` | string | Chain ID    | Yes       |

**Response Properties**

| Property      | Type   | Description                                |
| ------------- | ------ | ------------------------------------------ |
| `type`        | string | The Accumulate object type                 |
| `merkleState` | object | The merkle-state for this object           |
| `data`        | object | The data for this object (properties vary) |

**Example Request**

```cpp
curl -X POST --data '{
    "jsonrpc": "2.0",
    "id": 0,
    "method": "query-chain",
    "params": {
        "chainId": "12e2d2d82f7b65752b3fd8d37d195f6d87f6cb24b83c4ae70f4571ea1007e741"
    }
}' -H 'content-type:application/json;' https://testnet.accumulatenetwork.io/v2
```

**Example Response**

```d
{
    "jsonrpc": "2.0",
    "result": {
        "type": "keyPage",
        "merkleState": {
            "count": 1,
            "roots": [
                "cb0d7ccf124390693628c86cbb31cba64cee6c56b9086403f22c805b6bdf06d8"
            ]
        },
        "data": {
            "type": "keyPage",
            "url": "acc://kg1/prishth",
            "keyBook": "4b6fdf9d3e4ca631a0d1ca92eef528b7cfcd16a953efbe5e70811cd3841e88da",
            "managerKeyBook": "",
            "creditBalance": 0,
            "keys": [
                {
                    "publicKey": "57ddf8f09ddaaf28656fcca6ef1d4bb028c02ed31584c36df1e0ffcacc14d90c"
                }
            ]
        }
    },
    "id": 0
}
```

### query-data

Get data

**Request Parameters**

| Parameter   | Type   | Description | Required? |
| ----------- | ------ | ----------- | --------- |
| `url`       | string | URL         | Yes       |
| `entryHash` | string | URL         | No        |

**Response Properties**

| Property      | Type   | Description                                |
| ------------- | ------ | ------------------------------------------ |
| `type`        | string | The Accumulate object type                 |
| `merkleState` | object | The merkle-state for this object           |
| `data`        | object | The data for this object (properties vary) |

**Example Request**

```cpp
curl -X POST --data '{
    "jsonrpc": "2.0",
    "id": 0,
    "method": "query-data",
    "params": {
        "url": "acc://aditwo/aditwodata"
    }
}' -H 'content-type:application/json;' https://testnet.accumulatenetwork.io/v2
```

**Example Response**

```d
{
    "jsonrpc": "2.0",
    "result": {
        "type": "dataEntry",
        "merkleState": {
            "count": 2,
            "roots": [
                null,
                "87c5cc4a4f86accac328b5773c3e6fe29e8af23cbaa5a14f154011e2e71af4d2"
            ]
        },
        "data": {
            "entryHash": "b45fa53718dbc5bf31f2f6134d1ff84fe22b3760face9c2ab012fd66d16d1808",
            "entry": {
                "data": "61646974776f64617461"
            }
        }
    },
    "id": 0
}
```

### query-data-set

Get data set

**Request Parameters**

| Parameter | Type   | Description | Required? |
| --------- | ------ | ----------- | --------- |
| `url`     | string | URL         | Yes       |
| `count`   | int    | URL         | Yes       |

**Response Properties**

| Property | Type   | Description                |
| -------- | ------ | -------------------------- |
| `type`   | string | The Accumulate object type |
| `start`  | int    |                            |
| `count`  | int    |                            |
| `total`  | int    |                            |

**Example Request**

```cpp
curl -X POST --data '{
    "jsonrpc": "2.0",
    "id": 0,
    "method": "query-data-set",
    "params": {
        "url": "fun",
        "count":1
    }
}' -H 'content-type:application/json;' https://testnet.accumulatenetwork.io/v2
```

**Example Response**

```d
{
    "jsonrpc": "2.0",
    "result": {
        "type": "dataSet",
        "start": 0,
        "count": 1,
        "total": 0
    },
    "id": 0
}
```

### query-directory

Get directory information

**Request Parameters**

| Parameter | Type   | Description | Required? |
| --------- | ------ | ----------- | --------- |
| `url`     | string | URL         | Yes       |

**Response Properties**

| Property | Type   | Description                |
| -------- | ------ | -------------------------- |
| `type`   | string | The Accumulate object type |
| `start`  | int    |                            |
| `count`  | int    |                            |
| `total`  | int    |                            |

**Example Request**

```cpp
curl -X POST --data '{
    "jsonrpc": "2.0",
    "id": 0,
    "method": "query-directory",
    "params": {
        "url": "fun"
    }
}' -H 'content-type:application/json;' https://testnet.accumulatenetwork.io/v2
```

**Example Response**

```d
{
    "jsonrpc": "2.0",
    "result": {
        "type": "directory",
        "start": 0,
        "count": 1,
        "total": 4
    },
    "id": 0
}
```

### faucet

Get free ACME tokens. While supplies last!

**Request Parameters**

| Parameter | Type   | Description       | Required? |
| --------- | ------ | ----------------- | --------- |
| `url`     | string | Token account URL | Yes       |

**Response Properties**

| Property  | Type   | Description         |
| --------- | ------ | ------------------- |
| `txid`    | string | The transasction ID |
| `hash`    | string | Token Transaction   |
| `message` | string | The success Message |

**Example Request**

```cpp
curl -X POST --data '{
    "jsonrpc": "2.0",
    "id": 0,
    "method": "faucet",
    "params": {
        "url": "acc://5fd54e898c2c60e9757d2cd36f3a14b6df895b237690afb1/ACME"
    }
}' -H 'content-type:application/json;' https://testnet.accumulatenetwork.io/v2
```

**Example Response**

```d
{
    "jsonrpc": "2.0",
    "result": {
        "hash": "be347539c19cb0d5e1b396b4142a637ff94aec795e6e81442d37fe73469bc5dd",
        "message": "CheckTx",
        "txid": "7ec47e5a48e7b6e38040748885a9702ef1949b45325ac5eafd0f616457e92cda"
    },
    "id": 0
}
```

### query-key-index

Returns the specified key page / signature specification

**Request Parameters**

| Parameter | Type   | Description             | Required? |
| --------- | ------ | ----------------------- | --------- |
| `url`     | string | Accumulate Key Page URL | Yes       |
| `key`     | string | hash of public key      | Yes       |

**Response Properties**

| Property | Type   | Description                                |
| -------- | ------ | ------------------------------------------ |
| `type`   | string | The Accumulate object type                 |
| `data`   | object | The data for this object (properties vary) |

**Example Request**

```cpp
curl -X POST --data '{
    "jsonrpc": "2.0",
    "id": 0,
    "method": "query-key-index",
    "params": {
        "url": "acc://adione/page0",
        "key": "06b03ad284d26d249f99bed19586a1f314c72eb5bb37b55b22aaaacbe9c9b80f"
    }
}' -H 'content-type:application/json;' https://testnet.accumulatenetwork.io/v2
```

**Example Response**

```d
{
    "jsonrpc": "2.0",
    "result": {
        "type": "key-page-index",
        "data": {
            "keyBook": "acc://adione/book0",
            "keyPage": "acc://adione/page0",
            "index": 0
        }
    },
    "id": 0
}
```

### describe

**Example Request**

```cpp
curl -X POST --data '{
    "jsonrpc": "2.0",
    "id": 0,
    "method": "describe",
}' -H 'content-type:application/json;' https://testnet.accumulatenetwork.io/v2
```

**Example Response**

```d
{
    "jsonrpc": "2.0",
    "result": {
        "subnet": {
            "Type": "block-validator",
            "ID": "BVN2",
            "BvnNames": [
                "BVN0",
                "BVN1",
                "BVN2"
            ],
            "Addresses": {
                "bvn0": [
                    "http://127.0.100.5:26656",
                    "http://127.0.100.6:26656",
                    "http://127.0.100.7:26656",
                    "http://127.0.100.8:26656"
                ],
                "bvn1": [
                    "http://127.0.100.9:26656",
                    "http://127.0.100.10:26656",
                    "http://127.0.100.11:26656",
                    "http://127.0.100.12:26656"
                ],
                "bvn2": [
                    "http://127.0.100.13:26656",
                    "http://127.0.100.14:26656",
                    "http://127.0.100.15:26656",
                    "http://127.0.100.16:26656"
                ],
                "directory": [
                    "http://127.0.100.1:26656",
                    "http://127.0.100.2:26656",
                    "http://127.0.100.3:26656",
                    "http://127.0.100.4:26656"
                ]
            }
        }
    },
    "id": 0
}
```

### version

**Example Request**

```cpp
curl -X POST --data '{
    "jsonrpc": "2.0",
    "id": 0,
    "method": "version",
}' -H 'content-type:application/json;' https://testnet.accumulatenetwork.io/v2
```

**Example Response**

```d
{
    "jsonrpc": "2.0",
    "result": {
        "type": "version",
        "data": {
            "version": "v0.4.0-4-ge0866b72",
            "commit": "e0866b72bcb428e9c850ce8467197fc827f071bc",
            "versionIsKnown": true
        }
    },
    "id": 0
}
```

## Create methods

### create-adi

Creates a new ADI (Accumulate Digital Identity)

**Request Parameters**

| Parameter   | Type   | Description                                  | Required? |
| ----------- | ------ | -------------------------------------------- | --------- |
| `origin`    | string | The origin account                           | Yes       |
| `sponsor`   | string | The data for this object (properties vary)   | Yes       |
| `signer`    | object | ADI signing this request                     | Yes       |
| `signature` | string | Signature of the ADI signing the transaction | Yes       |
| `keyPage`   | object | The keypage for this object                  | Yes       |
| `payload`   | object | The data for this object (properties vary)   | Yes       |

**Response Properties**

| Property          | Type   | Description       |
| ----------------- | ------ | ----------------- |
| `transactionHash` | string | Transaction Hash  |
| `txid`            | string | Transaction ID    |
| `envelopeHash`    | string | Envelope Hash     |
| `simpleHash`      | string | Simple Hash       |
| `hash`            | string | Token Transaction |

**Example Request**

```cpp
curl -X POST --data '{
    "jsonrpc": "2.0",
    "id": 0,
    "method": "create-adi",
    "params": {
        "origin":"acc://5f1ad125de4275e18f0f8867bcb2a2103b2e44298650ec61/ACME",
        "sponsor":"acc://5f1ad125de4275e18f0f8867bcb2a2103b2e44298650ec61/ACME",
        "signer":{
            "publicKey":"0f1d20afd36f778df9692efa5b69bcf04adfe8cf7a4c12e50e4523bebab52825",
            "nonce":1642405755442626
        },"signature":"433b80aa4be172d05c55f86bf6aca5313c7a6a2c76784ac92d109420a18e6a5bb11a411e78b2ea437c4d83eca139d918fb414f01ab36782e81eb2b69ba5d6407",
        "keyPage":{"height":1},
        "payload":{
            "url":"pun8",
            "publicKey":"31c52df25166098c9f227e5bd4d39e1ef5c0ab9a6c4fcc327f27e3e38eab44b6",
            "keyBookName":"pun5book",
            "keyPageName":"pun5page"
        }
    }
}' -H 'content-type:application/json;' https://testnet.accumulatenetwork.io/v2
```

**Example Response**

```d
{
    "jsonrpc": "2.0",
    "result": {
        "transactionHash": "5938024f0957598dac26131a8669079e1626e698131deca05a1000c7f1f185c1",
        "txid": "5938024f0957598dac26131a8669079e1626e698131deca05a1000c7f1f185c1",
        "envelopeHash": "02dfa2dce7ea552e5762a8b3edbe4c2bd41ae6580cfff332e83350e703397d10",
        "simpleHash": "b6487f7599677e2aa33d3c2cc7b76258e06f0004943fe8cc48f1c7025820babd",
        "hash": "b6487f7599677e2aa33d3c2cc7b76258e06f0004943fe8cc48f1c7025820babd"
    },
    "id": 0
}
```

### create-data-account

Creates a new data account under an ADI

**Request Parameters**

| Parameter   | Type   | Description                                  | Required? |
| ----------- | ------ | -------------------------------------------- | --------- |
| `origin`    | string | The origin account                           | Yes       |
| `sponsor`   | string | The data for this object (properties vary)   | Yes       |
| `signer`    | object | ADI signing this request                     | Yes       |
| `signature` | string | Signature of the ADI signing the transaction | Yes       |
| `keyPage`   | object | The keypage for this object                  | Yes       |
| `payload`   | object | The data for this object (properties vary)   | Yes       |

**Response Properties**

| Property          | Type   | Description       |
| ----------------- | ------ | ----------------- |
| `transactionHash` | string | Transaction Hash  |
| `txid`            | string | Transaction ID    |
| `envelopeHash`    | string | Envelope Hash     |
| `simpleHash`      | string | Simple Hash       |
| `hash`            | string | Token Transaction |

**Example Request**

```cpp
curl -X POST --data '{
    "jsonrpc": "2.0",
    "id": 0,
    "method": "create-data-account",
    "params": {
        "origin":"acc://pun1",
        "sponsor":"acc://pun1",
        "signer":{
            "publicKey":"31c52df25166098c9f227e5bd4d39e1ef5c0ab9a6c4fcc327f27e3e38eab44b6",
            "nonce":1642415962518690
        },"signature":"be51cb7dcacd38943bb7d18e72b360e79ac1533ae933de76e7071db4f91d660ecad134808688e0c69d34ead11fbe2f6751dbbceedf8f74448635bd7aa5e0b60b",
        "keyPage":{"height":1},
        "payload":{
            "url":"acc://pun1/data",
            "keyBookUrl":"acc://pun1/pun1book"
        }
    }
}' -H 'content-type:application/json;' https://testnet.accumulatenetwork.io/v2
```

**Example Response**

```d
{
    "jsonrpc": "2.0",
    "result": {
        "transactionHash": "e0b10b09bb3215e3890c69cda6c41d41f46912d38fb0738dd0b4d146002b7d9b",
        "txid": "e0b10b09bb3215e3890c69cda6c41d41f46912d38fb0738dd0b4d146002b7d9b",
        "envelopeHash": "de5cba0bb00e7138ccf067fc6cb9485791ea646161850f6d5ab35809bb61d418",
        "simpleHash": "5f8869ce49529973546d78ffc6b5a48416b20bb6b655c56e9b0322ae258ecfaa",
        "hash": "5f8869ce49529973546d78ffc6b5a48416b20bb6b655c56e9b0322ae258ecfaa"
    },
    "id": 0
}
```

### create-token-account

Creates a new token account for an ADI

**Request Parameters**

| Parameter   | Type   | Description                                  | Required? |
| ----------- | ------ | -------------------------------------------- | --------- |
| `origin`    | string | The origin account                           | Yes       |
| `sponsor`   | string | The data for this object (properties vary)   | Yes       |
| `signer`    | object | ADI signing this request                     | Yes       |
| `signature` | string | Signature of the ADI signing the transaction | Yes       |
| `keyPage`   | object | The keypage for this object                  | Yes       |
| `payload`   | object | The data for this object (properties vary)   | Yes       |

**Response Properties**

| Property  | Type   | Description         |
| --------- | ------ | ------------------- |
| `hash`    | string | Token Transaction   |
| `txid`    | string | The transasction ID |
| `message` | string | The success Message |

**Example Request**

```cpp
curl -X POST --data '{
    "jsonrpc": "2.0",
    "id": 0,
    "method": "create-token-account",
    "params": {
        "origin":"acc://pun1",
        "sponsor":"acc://pun1",
        "signer":{
            "publicKey":"31c52df25166098c9f227e5bd4d39e1ef5c0ab9a6c4fcc327f27e3e38eab44b6",
            "nonce":1642416249257761
        },"signature":"8f70fd61875ee45e4743d0199a5705f19901cb6f34f65fe3fab7e5c07f86008dba656d04dfe2fda8d9e659610716938b8131560c3aaf34c2c45cad2204873605",
        "keyPage":{"height":1},
        "payload":{
            "url":"acc://pun1/tok",
            "tokenUrl":"acc://ACME",
            "keyBookUrl":"acc://pun1/pun1book"
        }
    }
}' -H 'content-type:application/json;' https://testnet.accumulatenetwork.io/v2
```

**Example Response**

```d
{
    "jsonrpc": "2.0",
    "result": {
        "hash": "95e68aad1ec44592514d64a4fd9747f8226282ff6d96784ee23bd5f7aaee4640",
        "message": "CheckTx",
        "txid": "1df91e761955e66cd8abbdf1caef8a4666db3746c69343382572451225d61807"
    },
    "id": 0
}
```

### create-key-page

Creates a new Key Page

**Request Parameters**

| Parameter   | Type   | Description                                  | Required? |
| ----------- | ------ | -------------------------------------------- | --------- |
| `origin`    | string | The origin account                           | Yes       |
| `sponsor`   | string | The data for this object (properties vary)   | Yes       |
| `signer`    | object | ADI signing this request                     | Yes       |
| `signature` | string | Signature of the ADI signing the transaction | Yes       |
| `keyPage`   | object | The keypage for this object                  | Yes       |
| `payload`   | object | The data for this object (properties vary)   | Yes       |

**Response Properties**

| Property          | Type   | Description       |
| ----------------- | ------ | ----------------- |
| `transactionHash` | string | Transaction Hash  |
| `txid`            | string | Transaction ID    |
| `envelopeHash`    | string | Envelope Hash     |
| `simpleHash`      | string | Simple Hash       |
| `hash`            | string | Token Transaction |

**Example Request**

```cpp
curl -X POST --data '{
    "jsonrpc": "2.0",
    "id": 0,
    "method": "create-key-page",
    "params": {
        "origin":"acc://pun123",
        "sponsor":"acc://pun123",
        "signer":{
            "publicKey":"31c52df25166098c9f227e5bd4d39e1ef5c0ab9a6c4fcc327f27e3e38eab44b6",
            "nonce":1642419400242766
        },"signature":"215ecd3c35da005687fa8eb54139067c9f5bbfe5e200a5a5b54e0f43492cbbd0dba47ab8814a21124f264fd85a6e9d54688275550d3adc45a5bdd3c4c82f1508",
        "keyPage":{"height":1},
        "payload":{
            "url":"acc://pun123/pg123",
            "keys":[{"publicKey":"31c52df25166098c9f227e5bd4d39e1ef5c0ab9a6c4fcc327f27e3e38eab44b6"}]
        }
    }
}' -H 'content-type:application/json;' https://testnet.accumulatenetwork.io/v2
```

**Example Response**

```d
{
    "jsonrpc": "2.0",
    "result": {
        "transactionHash": "75a0a6f0b6d196a22d1ecb66817c0fb72386ef34890f69b5cf6fa4745ef871f7",
        "txid": "75a0a6f0b6d196a22d1ecb66817c0fb72386ef34890f69b5cf6fa4745ef871f7",
        "envelopeHash": "0c1c2b2f1e7dd2acbe6a50f8bb7cbfdd715a938d24c057ed1546e1d48123d7a2",
        "simpleHash": "8601f63f80ff373050b02bb45ab6f3c174b1aa82f2ffb50959ad2be803a0a213",
        "hash": "8601f63f80ff373050b02bb45ab6f3c174b1aa82f2ffb50959ad2be803a0a213"
    },
    "id": 0
}
```

### update-key-page

Update key in a key page with a new public key

**Request Parameters**

| Parameter   | Type   | Description                                  | Required? |
| ----------- | ------ | -------------------------------------------- | --------- |
| `origin`    | string | The origin account                           | Yes       |
| `sponsor`   | string | The data for this object (properties vary)   | Yes       |
| `signer`    | object | ADI signing this request                     | Yes       |
| `signature` | string | Signature of the ADI signing the transaction | Yes       |
| `keyPage`   | object | The keypage for this object                  | Yes       |
| `payload`   | object | The data for this object (properties vary)   | Yes       |

**Response Properties**

| Property          | Type   | Description       |
| ----------------- | ------ | ----------------- |
| `transactionHash` | string | Transaction Hash  |
| `txid`            | string | Transaction ID    |
| `envelopeHash`    | string | Envelope Hash     |
| `simpleHash`      | string | Simple Hash       |
| `hash`            | string | Token Transaction |

**Example Request**

```cpp
curl -X POST --data '{
    "jsonrpc": "2.0",
    "id": 0,
    "method": "update-key-page",
    "params": {
        "origin":"acc://fun/funpage",
        "sponsor":"acc://fun/funpage",
        "signer":{
            "publicKey":"313cfdb8a47c302d1622f5a7c064fa312935579fbac867c3cfc764617b151d5c",
            "nonce":1643889342338447
        },"signature":"871e18e8bde6f97b8a49323a958405b8f7499afee83294f6ff05236f6f5e1f96ec11ed3fe01928c8685efd7995a96ad634ebc6dc26e67a1a0be64522294c6f02",
        "keyPage":{"height":7},
        "payload":{
            "operation":"update",
            "key":"313cfdb8a47c302d1622f5a7c064fa312935579fbac867c3cfc764617b151d5c",
            "newKey":"06b03ad284d26d249f99bed19586a1f314c72eb5bb37b55b22aaaacbe9c9b80f"
        }
    }
}' -H 'content-type:application/json;' https://testnet.accumulatenetwork.io/v2
```

**Example Response**

```d
{
    "jsonrpc": "2.0",
    "result": {
        "transactionHash": "e7d8cd07d3d9fa64ffd537730df6fdbc20e2214342d7a919d7bc2e16f0a96324",
        "txid": "e7d8cd07d3d9fa64ffd537730df6fdbc20e2214342d7a919d7bc2e16f0a96324",
        "envelopeHash": "e8594157bff23451f50429a3e4fc7399f9dbc177728a54341dc713a66603481a",
        "simpleHash": "2ff5705a0e4c604de62a3f867d8c4f821341d77359714c7271ab3877e3b73622",
        "hash": "2ff5705a0e4c604de62a3f867d8c4f821341d77359714c7271ab3877e3b73622"
    },
    "id": 0
}
```

### create-key-book

Creates a new Key Book

**Request Parameters**

| Parameter   | Type   | Description                                  | Required? |
| ----------- | ------ | -------------------------------------------- | --------- |
| `origin`    | string | The origin account                           | Yes       |
| `sponsor`   | string | The data for this object (properties vary)   | Yes       |
| `signer`    | object | ADI signing this request                     | Yes       |
| `signature` | string | Signature of the ADI signing the transaction | Yes       |
| `keyPage`   | object | The keypage for this object                  | Yes       |
| `payload`   | object | The data for this object (properties vary)   | Yes       |

**Response Properties**

| Property          | Type   | Description       |
| ----------------- | ------ | ----------------- |
| `transactionHash` | string | Transaction Hash  |
| `txid`            | string | Transaction ID    |
| `envelopeHash`    | string | Envelope Hash     |
| `simpleHash`      | string | Simple Hash       |
| `hash`            | string | Token Transaction |

**Example Request**

```cpp
curl -X POST --data '{
    "jsonrpc": "2.0",
    "id": 0,
    "method": "create-key-page",
    "params": {
        "origin":"acc://pun123",
        "sponsor":"acc://pun123",
        "signer":{
            "publicKey":"31c52df25166098c9f227e5bd4d39e1ef5c0ab9a6c4fcc327f27e3e38eab44b6",
            "nonce":1642419179442424
        },"signature":"99c00392160d00586c3e82f966d6452bb9758e11add68a6c39c3d08ee27006afb07f88f7c21288ed48cb848d9f7ca5968f54d2b51173f84f4e0057f5c785d50b",
        "keyPage":{"height":1},
        "payload":{
            "url":"acc://pun123/book0",
            "pages":["76037579e7e45b863ef34705c9931a5191faa01e85088a8e636d5f70472e0730"]
        }
    }
}' -H 'content-type:application/json;' https://testnet.accumulatenetwork.io/v2
```

**Example Response**

```d
{
    "jsonrpc": "2.0",
    "result": {
        "transactionHash": "5a17b09ca070305f7797ff18af6ddf27b483b311b5451ffbd9ab242deb9f7400",
        "txid": "5a17b09ca070305f7797ff18af6ddf27b483b311b5451ffbd9ab242deb9f7400",
        "envelopeHash": "c27fabdf0a6a118ac660b1b53517ec0bd06fd34e47d9f8e3237a1d1ec0c53097",
        "simpleHash": "4653e636a6b0f867c2d273c7ed8923df12e3493bc649d8e106a98c9b8915be51",
        "hash": "4653e636a6b0f867c2d273c7ed8923df12e3493bc649d8e106a98c9b8915be51"
    },
    "id": 0
}
```

### write-data

Write entry to a data account

**Request Parameters**

| Parameter   | Type   | Description                                  | Required? |
| ----------- | ------ | -------------------------------------------- | --------- |
| `origin`    | string | The origin account                           | Yes       |
| `sponsor`   | string | The data for this object (properties vary)   | Yes       |
| `signer`    | object | ADI signing this request                     | Yes       |
| `signature` | string | Signature of the ADI signing the transaction | Yes       |
| `keyPage`   | object | The keypage for this object                  | Yes       |
| `payload`   | object | The data for this object (properties vary)   | Yes       |

**Response Properties**

| Property          | Type   | Description       |
| ----------------- | ------ | ----------------- |
| `transactionHash` | string | Transaction Hash  |
| `txid`            | string | Transaction ID    |
| `envelopeHash`    | string | Envelope Hash     |
| `simpleHash`      | string | Simple Hash       |
| `hash`            | string | Token Transaction |

**Example Request**

```cpp
curl -X POST --data '{
    "jsonrpc": "2.0",
    "id": 0,
    "method": "write-data",
    "params": {
        "origin":"acc://pun1/data",
        "sponsor":"acc://pun1/data",
        "signer":{
            "publicKey":"31c52df25166098c9f227e5bd4d39e1ef5c0ab9a6c4fcc327f27e3e38eab44b6",
            "nonce":1642419054067056
        },"signature":"19795c8bd66ed8c247568e98d0c19d8498c01247191a12c337e1d02f53fcf2121bb93c16a1fe5cdb5ec33fbac415fd55dd76d84457fd508888fe00ce43f47d0d",
        "keyPage":{"height":1},
        "payload":{
            "entry":{"data":"7465737464617461"}
        }
    }
}' -H 'content-type:application/json;' https://testnet.accumulatenetwork.io/v2
```

**Example Response**

```d
{
    "jsonrpc": "2.0",
    "result": {
        "hash": "4e1cb535ffa781b404ad7a05d0b771c76696a95555d063d9958ea90a88a4d6a3",
        "message": "CheckTx",
        "txid": "56362a342374d68b51883e85f0dbaa2ba601fd0f1dbb3a11d3506864f721e796"
    },
    "id": 0
}
```

### write-data-to

Write entry to a data account

**Request Parameters**

| Parameter   | Type   | Description                                  | Required? |
| ----------- | ------ | -------------------------------------------- | --------- |
| `origin`    | string | The origin account                           | Yes       |
| `sponsor`   | string | The data for this object (properties vary)   | Yes       |
| `signer`    | object | ADI signing this request                     | Yes       |
| `signature` | string | Signature of the ADI signing the transaction | Yes       |
| `keyPage`   | object | The keypage for this object                  | Yes       |
| `payload`   | object | The data for this object (properties vary)   | Yes       |

**Response Properties**

| Property  | Type   | Description         |
| --------- | ------ | ------------------- |
| `hash`    | string | Token Transaction   |
| `txid`    | string | The transasction ID |
| `message` | string | The success Message |

**Example Request**

```cpp
curl -X POST --data '{
    "jsonrpc": "2.0",
    "id": 0,
    "method": "write-data-to",
    "params": {
        "origin":"acc://fun",
        "sponsor":"acc://fun",
        "signer":{
            "publicKey":"06b03ad284d26d249f99bed19586a1f314c72eb5bb37b55b22aaaacbe9c9b80f",
            "nonce":1643890491830725
        },"signature":"51cc66214c6173fba699d56c986f7444705b2cfaf4ecff5236d2970b7c3d90ffb45def706119fd1b8b382c12882c380671c2a7fb340d11e830bcd009773da10b",
        "keyPage":{"height":8},
        "payload":{
            "recipient":"acc://a46c76c16addf3177fa48ffc2ff4dae791a6dc669da9fd4a",
            "entry":{"data":"7465737464617461"}
        }
    }
}' -H 'content-type:application/json;' https://testnet.accumulatenetwork.io/v2
```

**Example Response**

```d
{
    "jsonrpc": "2.0",
    "result": {
        "transactionHash": "e7d8cd07d3d9fa64ffd537730df6fdbc20e2214342d7a919d7bc2e16f0a96324",
        "txid": "e7d8cd07d3d9fa64ffd537730df6fdbc20e2214342d7a919d7bc2e16f0a96324",
        "envelopeHash": "e8594157bff23451f50429a3e4fc7399f9dbc177728a54341dc713a66603481a",
        "simpleHash": "2ff5705a0e4c604de62a3f867d8c4f821341d77359714c7271ab3877e3b73622",
        "hash": "2ff5705a0e4c604de62a3f867d8c4f821341d77359714c7271ab3877e3b73622"
    },
    "id": 0
}
```

### create-token

Create token

**Request Parameters**

| Parameter   | Type   | Description                                  | Required? |
| ----------- | ------ | -------------------------------------------- | --------- |
| `origin`    | string | The origin account                           | Yes       |
| `sponsor`   | string | The data for this object (properties vary)   | Yes       |
| `signer`    | object | ADI signing this request                     | Yes       |
| `signature` | string | Signature of the ADI signing the transaction | Yes       |
| `keyPage`   | object | The keypage for this object                  | Yes       |
| `payload`   | object | The data for this object (properties vary)   | Yes       |

**Response Properties**

| Property          | Type   | Description       |
| ----------------- | ------ | ----------------- |
| `transactionHash` | string | Transaction Hash  |
| `txid`            | string | Transaction ID    |
| `envelopeHash`    | string | Envelope Hash     |
| `simpleHash`      | string | Simple Hash       |
| `hash`            | string | Token Transaction |

**Example Request**

```cpp
curl -X POST --data '{
    "jsonrpc": "2.0",
    "id": 0,
    "method": "create-token",
    "params": {
        "origin":"acc://fun",
        "sponsor":"acc://fun",
        "signer":{
            "publicKey":"06b03ad284d26d249f99bed19586a1f314c72eb5bb37b55b22aaaacbe9c9b80f",
            "nonce":1643908516407232
        },"signature":"ea6d8f1797861480890e6cacb8c32917411a1799d8345b2965f6e338dac7ff584a95c29b09c5d19ec371b295e1555f27898f7a5bc00f568741d4177d7eb82b0b",
        "keyPage":{"height":11},
        "payload":{
            "url":"acc://fun/funtoken",
            "symbol":ft,
            "precision":2,
            "initialSupply":"0"
            }
    }
}' -H 'content-type:application/json;' https://testnet.accumulatenetwork.io/v2
```

**Example Response**

```d
{
    "jsonrpc": "2.0",
    "result": {
        "transactionHash": "5a0a1f30e21dcac73ad9999bc825ec04b608344e98a43bc5383bc1c00473db16",
        "txid": "5a0a1f30e21dcac73ad9999bc825ec04b608344e98a43bc5383bc1c00473db16",
        "envelopeHash": "3802c9c17542cb9ffb3934ae9a8870fc99a34ec1fbe0180f4245aed27ccf4878",
        "simpleHash": "c802830a48a03021d9f7fa8372dcd5efe78961de578965ea980659e22037cbce",
        "hash": "c802830a48a03021d9f7fa8372dcd5efe78961de578965ea980659e22037cbce"
    },
    "id": 0
}
```

### issue-token

Issue token

**Request Parameters**

| Parameter   | Type   | Description                                  | Required? |
| ----------- | ------ | -------------------------------------------- | --------- |
| `origin`    | string | The origin account                           | Yes       |
| `sponsor`   | string | The data for this object (properties vary)   | Yes       |
| `signer`    | object | ADI signing this request                     | Yes       |
| `signature` | string | Signature of the ADI signing the transaction | Yes       |
| `keyPage`   | object | The keypage for this object                  | Yes       |
| `payload`   | object | The data for this object (properties vary)   | Yes       |

**Response Properties**

| Property          | Type   | Description       |
| ----------------- | ------ | ----------------- |
| `transactionHash` | string | Transaction Hash  |
| `txid`            | string | Transaction ID    |
| `envelopeHash`    | string | Envelope Hash     |
| `simpleHash`      | string | Simple Hash       |
| `hash`            | string | Token Transaction |

**Example Request**

```cpp
curl -X POST --data '{
    "jsonrpc": "2.0",
    "id": 0,
    "method": "issue-tokens",
    "params": {
        "origin":"acc://fun/funtoken",
        "sponsor":"acc://fun/funtoken",
        "signer":{
            "publicKey":"06b03ad284d26d249f99bed19586a1f314c72eb5bb37b55b22aaaacbe9c9b80f",
            "nonce":1643911774348012
        },"signature":"724985a4022419c6324d1933f0968e203c39e08d0eb244e53e63870786456c64896849051b31c7a24e2f537adf6a86b1dc29152515fb2862d4fa41a02085fb0d",
        "keyPage":{"height":15},
        "payload":{
            "recipient":"acc://fun/funAccToken",
            "amount":"10"
            }
    }
}' -H 'content-type:application/json;' https://testnet.accumulatenetwork.io/v2
```

**Example Response**

```d
{
    "jsonrpc": "2.0",
    "result": {
        "transactionHash": "2b4e43d21361cc3aa47bd6b4fb813aaef2f91c7df692e46e2a8cf8e77d0348f3",
        "txid": "2b4e43d21361cc3aa47bd6b4fb813aaef2f91c7df692e46e2a8cf8e77d0348f3",
        "envelopeHash": "793da8890631ae04caed1fd90a8b1d0ca986d21249d8fc64d84de399b8d79c09",
        "simpleHash": "9adf795c9f7b919c5ab0d97554e90d96bf1631d87b6c556920da5cf5f482d886",
        "hash": "9adf795c9f7b919c5ab0d97554e90d96bf1631d87b6c556920da5cf5f482d886"
    },
    "id": 0
}
```

### burn-tokens

Burn token

**Request Parameters**

| Parameter   | Type   | Description                                  | Required? |
| ----------- | ------ | -------------------------------------------- | --------- |
| `origin`    | string | The origin account                           | Yes       |
| `sponsor`   | string | The data for this object (properties vary)   | Yes       |
| `signer`    | object | ADI signing this request                     | Yes       |
| `signature` | string | Signature of the ADI signing the transaction | Yes       |
| `keyPage`   | object | The keypage for this object                  | Yes       |
| `payload`   | object | The data for this object (properties vary)   | Yes       |

**Response Properties**

| Property          | Type   | Description       |
| ----------------- | ------ | ----------------- |
| `transactionHash` | string | Transaction Hash  |
| `txid`            | string | Transaction ID    |
| `envelopeHash`    | string | Envelope Hash     |
| `simpleHash`      | string | Simple Hash       |
| `hash`            | string | Token Transaction |

**Example Request**

```cpp
curl -X POST --data '{
    "jsonrpc": "2.0",
    "id": 0,
    "method": "burn-tokens",
    "params": {
        "origin":"acc://09bca3fcd7e28434f4fb5a3c7317d64e955acbc102e45df5/ACME",
        "sponsor":"acc://09bca3fcd7e28434f4fb5a3c7317d64e955acbc102e45df5/ACME",
        "signer":{
            "publicKey":"699bf621792c70fcabe70efaa6eb5fab451b9eaf2053fb0a66d110209b1f5cf4",
            "nonce":1644429190391471
        },"signature":"a5faa201c49ba24a2655e0e3263732237663a9dba83e215e2fe992c6b52af0fa58b4f35e096ddcc057b556f40c89ae9595e6b36259a74fea6f5d960951282600",
        "keyPage":{
            "height":1,
            "index":0
            },
        "payload":{
            "amount":"100000000"
            }
    }
}' -H 'content-type:application/json;' https://testnet.accumulatenetwork.io/v2
```

**Example Response**

```d
{
    "jsonrpc": "2.0",
    "result": {
        "transactionHash": "047a9c71c04006129835667610d132698c0651270252dccbb31d6df48b25e8b1",
        "txid": "047a9c71c04006129835667610d132698c0651270252dccbb31d6df48b25e8b1",
        "envelopeHash": "54dc39ffc1812b2c74702696a050c768aaaebcc9592893051176c4ba2e3bc383",
        "simpleHash": "3b476be18b19c51eba2c18a93b8e0ac103be233a4fb66d5b18e945eb115ae630",
        "hash": "3b476be18b19c51eba2c18a93b8e0ac103be233a4fb66d5b18e945eb115ae630"
    },
    "id": 0
}
```

### send-tokens

Send tokens from one account to another

**Request Parameters**

| Parameter   | Type   | Description                                  | Required? |
| ----------- | ------ | -------------------------------------------- | --------- |
| `origin`    | string | The origin account                           | Yes       |
| `sponsor`   | string | The data for this object (properties vary)   | Yes       |
| `signer`    | object | ADI signing this request                     | Yes       |
| `signature` | string | Signature of the ADI signing the transaction | Yes       |
| `keyPage`   | object | The keypage for this object                  | Yes       |
| `payload`   | object | The data for this object (properties vary)   | Yes       |

**Response Properties**

| Property  | Type   | Description         |
| --------- | ------ | ------------------- |
| `hash`    | string | Token Transaction   |
| `txid`    | string | The transasction ID |
| `message` | string | The success Message |

**Example Request**

```cpp
curl -X POST --data '{
    "jsonrpc": "2.0",
    "id": 0,
    "method": "send-tokens",
    "params": {
        "origin":"acc://5f1ad125de4275e18f0f8867bcb2a2103b2e44298650ec61/ACME",
        "sponsor":"acc://5f1ad125de4275e18f0f8867bcb2a2103b2e44298650ec61/ACME",
        "signer":{
            "publicKey":"0f1d20afd36f778df9692efa5b69bcf04adfe8cf7a4c12e50e4523bebab52825",
            "nonce":1642421667051758
        },"signature":"b3e4729436359ecdc5736998205a425d0e8740eede791b620b7abd2eb88d0b8d4ae1822811e2de6b3509e949dff3d67767340973e97601f05876fe54af81f606",
        "keyPage":{"height":1},
        "payload":{
            "hash":"0000000000000000000000000000000000000000000000000000000000000000",
            "to":[{"url":"acc://595f9bf47adae283e98a6ddaf466b733d1ae6127711313f2/ACME","amount":1000000000}]
            }
    }
}' -H 'content-type:application/json;' https://testnet.accumulatenetwork.io/v2
```

**Example Response**

```d
{
    "jsonrpc": "2.0",
    "result": {
        "hash": "848245dc249b266a238004cb3b8c574435089f0e0618f2bab3c3f2c7738632b6",
        "message": "CheckTx",
        "txid": "839eb76679b2132bb52f369bfb9ddcd57bc716cc4a2a67da00fc679610847328"
    },
    "id": 0
}
```

### add-credits

Send Credits from one account to another

**Request Parameters**

| Parameter   | Type   | Description                                  | Required? |
| ----------- | ------ | -------------------------------------------- | --------- |
| `origin`    | string | The origin account                           | Yes       |
| `sponsor`   | string | The data for this object (properties vary)   | Yes       |
| `signer`    | object | ADI signing this request                     | Yes       |
| `signature` | string | Signature of the ADI signing the transaction | Yes       |
| `keyPage`   | object | The keypage for this object                  | Yes       |
| `payload`   | object | The data for this object (properties vary)   | Yes       |

**Response Properties**

| Property  | Type   | Description         |
| --------- | ------ | ------------------- |
| `hash`    | string | Token Transaction   |
| `txid`    | string | The transasction ID |
| `message` | string | The success Message |

**Example Request**

```cpp
curl -X POST --data '{
    "jsonrpc": "2.0",
    "id": 0,
    "method": "add-credits",
    "params": {
        "origin":"acc://595f9bf47adae283e98a6ddaf466b733d1ae6127711313f2/ACME",
        "sponsor":"acc://595f9bf47adae283e98a6ddaf466b733d1ae6127711313f2/ACME",
        "signer":{
            "publicKey":"becbf8ba73bae227853e9e6e7ffbb5689d7022b070ef95f99e0cc879b7b56a0b",
            "nonce":1642422094810161
        },"signature":"0c5d0ba22bc21b542a11db233d326f6a580c7a26dc815bd76a0297f33b716b0530658ac005111ed81efd2002a39e7825cf5c9d65cf7941b90b12af5252bcfe0d",
        "keyPage":{"height":1},
        "payload":{
            "recipient":"acc://5f1ad125de4275e18f0f8867bcb2a2103b2e44298650ec61/ACME",
            "amount":5}
        }
}' -H 'content-type:application/json;' https://testnet.accumulatenetwork.io/v2
```

**Example Response**

```d
{
    "jsonrpc": "2.0",
    "result": {
        "hash": "e00dac5f3e279ce083a5b69fe7649f278e6613442ebfe54359e235a176b54a03",
        "message": "CheckTx",
        "txid": "3765f47b94a9fbb8a8ae012825e2c8cded47405306265078141e4bd6505292d9"
    },
    "id": 0
}
```

### update-manager

**Request Parameters**

| Parameter   | Type   | Description                                  | Required? |
| ----------- | ------ | -------------------------------------------- | --------- |
| `origin`    | string | The origin account                           | Yes       |
| `sponsor`   | string | The data for this object (properties vary)   | Yes       |
| `signer`    | object | ADI signing this request                     | Yes       |
| `signature` | string | Signature of the ADI signing the transaction | Yes       |
| `keyPage`   | object | The keypage for this object                  | Yes       |
| `payload`   | object | The data for this object (properties vary)   | Yes       |

**Response Properties**

| Property          | Type   | Description       |
| ----------------- | ------ | ----------------- |
| `transactionHash` | string | Transaction Hash  |
| `txid`            | string | Transaction ID    |
| `envelopeHash`    | string | Envelope Hash     |
| `simpleHash`      | string | Simple Hash       |
| `hash`            | string | Token Transaction |

**Example Request**

```cpp
curl -X POST --data '{
    "jsonrpc": "2.0",
    "id": 0,
    "method": "update-manager",
    "params": {
            "origin":"acc://testadi/page",
            "sponsor":"acc://testadi/page",
            "signer":{
                "publicKey":"06b03ad284d26d249f99bed19586a1f314c72eb5bb37b55b22aaaacbe9c9b80f",
                "nonce":1646848796500769
            },
            "signature":"bd99ad4929a27e01f0e1628bb5b6fef4cbf07acd0e80a1f9e434c071469149c123d299eb8d144c5dbf7895056ea3f4f43854bfaf160d89bc7900e77c4ad47306",
            "keyPage":{
                "height":3,
                "index":0
            },
            "payload":{
                "type":"updateManager",
                "managerKeyBook":"acc://testadi/book"
            }
            }
}' -H 'content-type:application/json;' https://testnet.accumulatenetwork.io/v2
```

**Example Response**

```d
{
    "jsonrpc": "2.0",
    "result": {
        "transactionHash": "9b98f65207b77c5a2e54243d624d8ff0da73ca5f90d7e6d22782cc6cd831e940",
        "txid": "9b98f65207b77c5a2e54243d624d8ff0da73ca5f90d7e6d22782cc6cd831e940",
        "envelopeHash": "39c2a18a96b4e6152e6837c7c1b4073d922b837084f6342f544113deed9f1157",
        "simpleHash": "a86fc3abd7097f03f8382e68d0985404db2d1559eaef0f00895df655b58baff8",
        "hash": "a86fc3abd7097f03f8382e68d0985404db2d1559eaef0f00895df655b58baff8"
    },
    "id": 0
}
```

### remove-manager

**Request Parameters**

| Parameter   | Type   | Description                                  | Required? |
| ----------- | ------ | -------------------------------------------- | --------- |
| `origin`    | string | The origin account                           | Yes       |
| `sponsor`   | string | The data for this object (properties vary)   | Yes       |
| `signer`    | object | ADI signing this request                     | Yes       |
| `signature` | string | Signature of the ADI signing the transaction | Yes       |
| `keyPage`   | object | The keypage for this object                  | Yes       |
| `payload`   | object | The data for this object (properties vary)   | Yes       |

**Response Properties**

| Property          | Type   | Description       |
| ----------------- | ------ | ----------------- |
| `transactionHash` | string | Transaction Hash  |
| `txid`            | string | Transaction ID    |
| `envelopeHash`    | string | Envelope Hash     |
| `simpleHash`      | string | Simple Hash       |
| `hash`            | string | Token Transaction |

**Example Request**

```cpp
curl -X POST --data '{
    "jsonrpc": "2.0",
    "id": 0,
    "method": "remove-manager",
    "params": {
            "origin":"acc://testadi/page",
            "sponsor":"acc://testadi/page",
            "signer":{
                "publicKey":"06b03ad284d26d249f99bed19586a1f314c72eb5bb37b55b22aaaacbe9c9b80f",
                "nonce":1646849056685160
            },
            "signature":"88c889b35d4d32b541ddf96c7582aef3f712bf30859ee7ce2816399f22461bfb300dca518c4748209851be94ce0d743bc6c35c8a76f41efc3f10ff542b114201",
            "keyPage":{
                "height":4,
                "index":0
            },
            "payload":{
                "type":"removeManager"
            }
            }
}' -H 'content-type:application/json;' https://testnet.accumulatenetwork.io/v2
```

**Example Response**

```d
{
    "jsonrpc": "2.0",
    "result": {
        "transactionHash": "a0409b7139c7fd7656488abe9896918812242bca538286f1433dfa73bc94a41f",
        "txid": "a0409b7139c7fd7656488abe9896918812242bca538286f1433dfa73bc94a41f",
        "envelopeHash": "3e1d26ebd4732a77d577ebfd311d12700945c677d30a7e5ddc045449d55e7f69",
        "simpleHash": "36045c816f90f514d8d5e8effd3b200366abde9270cb54386192fa15ef062b55",
        "hash": "36045c816f90f514d8d5e8effd3b200366abde9270cb54386192fa15ef062b55"
    },
    "id": 0
}
```
