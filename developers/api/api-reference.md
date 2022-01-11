# API Reference

### Format

This API uses the JSON-RPC 2.0 format. For more information on making JSON-RPC calls, see [Issuing API Calls](issuing-api-calls.md#json-rpc-formatted-apis).

### Endpoint

`[node-ip]:[http-port]/v1`

#### Testnet Endpoint

`https://testnet.accumulatenetwork.io/v2`

## Methods

### _URL methods_

### query

Returns Accumulate Object by URL

**Request Parameters**

| Parameter | Type   | Description        | Required? |
| --------- | ------ | ------------------ | --------- |
| `url`     | string | Any Accumulate URL | Yes       |

**Response Properties**

| Property      | Type   | Description                                                                     |
| ---------     | ------ | ------------------------------------------------------------------------------- |
| `type`        | string | The Accumulate object type                                                      |
| `merkleState` | object |                                                                                 |
| `data`        | object | The data for this object (properties vary)                                      |

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


### _ADI methods_

Returns information about the specified ADI


**Example Request**

```d
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

| Parameter | Type   | Description       | Required? |
| --------- | ------ | ----------------- | --------- |
| `url`     | string | Token Account URL | Yes       |
| `count`   | int    |                   | Yes       |

**Response Properties**

| Property          | Type   | Description       |
| ----------------- | ------ | ----------------- |
|                   |        |                   |

**Errors**

| Code   | Message                      |
| ------ | ---------------------------- |
|        |                              |
|        |                              |

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
        "items": [
            {
                "type": "syntheticDepositTokens",
                "data": {
                    "txid": "b735291bca4dfc28ae0c0092a688e5d75b5722cac225c6bfd5e9b2929a603467",
                    "from": "acc://7117c50f04f1254d56b704dc05298912deeb25dbc1d26ef6/ACME",
                    "to": "acc://5fd54e898c2c60e9757d2cd36f3a14b6df895b237690afb1/ACME",
                    "amount": "1000000000",
                    "tokenURL": "ACME"
                },
                "sponsor": "acc://7117c50f04f1254d56b704dc05298912deeb25dbc1d26ef6/ACME",
                "keyPage": {
                    "height": 1
                },
                "txid": "c7e59bfea5029963ee07c27a09e5e7467e30cd4ebc1822e16ebbb173a8ff685c",
                "signer": {
                    "publicKey": "14e97550afcace8082546d71001af1844fba07818c0624c2ce17b054f0260e45",
                    "nonce": 18446744073709551615
                },
                "sig": "1c0d7064e5e6ad77eb3ddbe39cf687fe75124415b7726b635d829276892c47fad7ec63ee6376fa5730845e0053c154c3f162016568ccd4f499e3fc881bac3302",
                "status": {
                    "code": "0"
                }
            }
        ],
        "start": 0,
        "count": 1,
        "total": 1
    },
    "id": 0
}
```

###

### query-tx

Returns transaction data for the specified transaction

**Request Parameters**

| Parameter | Type   | Description      | Required? |
| --------- | ------ | ---------------- | --------- |
| `txid`    | string | Transaction hash | Yes       |

**Response Properties**

| Property          | Type   | Description       |
| ----------------- | ------ | ----------------- |
| `tokenTxWithHash` | object | Token transaction |

**Errors**

| Code   | Message                    |
| ------ | -------------------------- |
| -34002 | Invalid transaction hash   |
| -34003 | Transaction does not exist |

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
        "type": "acmeFaucet",
        "data": {
            "url": "acc://cddfb7ce867972e41ae5aaca86db77292ca3170e2009d8f4/ACME"
        },
        "sponsor": "acc://7117c50f04f1254d56b704dc05298912deeb25dbc1d26ef6/ACME",
        "keyPage": {
            "height": 1
        },
        "txid": "9dce91ec75f5b5e767283d8db77394daeef6e50b4f0e1197624f1a888ed076b1",
        "signer": {
            "publicKey": "d03c683332ed36add8d0eeb9eee9e2669b5565decec03acc43d762f3f79f49c2",
            "nonce": 1641907412194963895
        },
        "sig": "962c97762149f346350b867aef604c168a088a6effbf987f3b0e05cb24095650df973f43989c3eb50cbbb903c30ad94991d46e5041d4220b400bb7bf946b7f0c",
        "status": {
            "code": "0"
        },
        "syntheticTxids": [
            "7c478d483a26192b84a637c674ea28ba6d71b16af011da325fa5eb160321697f"
        ]
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

| Property    | Type   | Description         |
| ----------- | ------ | ------------------- |
| `txid`      | string | The transasction ID |
| `hash`      | string |                     |
| `message`   | string |                     |

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

### _Key management methods_

### query-key-index

Returns the specified key page / signature specification

**Request Parameters**

| Parameter | Type   | Description             | Required? |
| --------- | ------ | ----------------------- | --------- |
| `url`     | string | Accumulate Key Page URL | Yes       |
| `key`     | string |                         | Yes       |

**Response Properties**

| Property  | Type   | Description                                                                                   |
| --------- | ------ | --------------------------------------------------------------------------------------------- |
| `keyPage` | object | An object containing the Chain URL, Key book ID, credit balance, and an unordered set of keys |

**Example Request**

```cpp
curl -X POST --data '{
    "jsonrpc": "2.0",
    "id": 0,
    "method": "query-key-index",
    "params": {
        "url": "acc://adione/page0"
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

###
