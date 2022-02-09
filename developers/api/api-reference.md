# API Reference

### Format

This API uses the JSON-RPC 2.0 format. For more information on making JSON-RPC calls, see [Issuing API Calls](issuing-api-calls.md#json-rpc-formatted-apis).

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

| Parameter | Type   | Description                      | Required? |
| --------- | ------ | -------------------------------- | --------- |
| `url`     | string | Token Account URL                | Yes       |
| `count`   | int    | Count of history trananctions    | Yes       |

**Response Properties**

| Property            | Type         | Description                                  |
| -----------------   | ------       | ----------------------------------------     |
| `type`              |  string      | The Accumulate object type                   |
| `data`              |  object      | The data for this object (properties vary)   |
| `sponsor`           |  string      | The data for this object (properties vary)   |
| `keypage`           |  object      | The Keypage for this object                  |
| `txid`              |  string      | Transaction hash                             |
| `signer`            |  object      | ADI signing the creation of new token        |
| `sig`               |  object      | Signature of the ADI signing the transaction |
| `status`            |  object      | Status                                       |


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

### query-tx

Returns transaction data for the specified transaction

**Request Parameters**

| Parameter | Type   | Description      | Required? |
| --------- | ------ | ---------------- | --------- |
| `txid`    | string | Transaction hash | Yes       |

**Response Properties**

| Property            | Type         | Description                                  |
| -----------------   | ------       | ----------------------------------------     |
| `type`              |  string      | The Accumulate object type                   |
| `data`              |  object      | The data for this object (properties vary)   |
| `sponsor`           |  string      | The data for this object (properties vary)   |
| `keypage`           |  object      | The Keypage for this object                  |
| `txid`              |  string      | Transaction hash                             |
| `signer`            |  object      | ADI signing the creation of new token        |
| `sig`               |  object      | Signature of the ADI signing the transaction |
| `status`            |  object      | Status                                       |

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

### query-chain

Get query-chain properties

**Request Parameters**

| Parameter     | Type      | Description       | Required? |
| ---------     | ------    | ----------------- | --------- |
| `chainId`     | string    | Chain ID          | Yes       |

**Response Properties**

| Property      | Type   | Description                                  |
| -----------   | ------ | --------------------------------------       |
| `type`        | string | The Accumulate object type                   |
| `merkleState` | object | The merkle-state for this object             |
| `data`        | object | The data for this object (properties vary)   |

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

| Parameter     | Type   | Description       | Required? |
| ---------     | ------ | ----------------- | --------- |
| `url`         | string | URL               | Yes       |
| `entryHash`   | string | URL               | No        |

**Response Properties**

| Property      | Type   | Description                                  |
| -----------   | ------ | --------------------------------------       |
| `type`        | string | The Accumulate object type                   |
| `merkleState` | object | The merkle-state for this object             |
| `data`        | object | The data for this object (properties vary)   |


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

| Parameter     | Type   | Description       | Required? |
| ---------     | ------ | ----------------- | --------- |
| `url`         | string | URL               | Yes       |
| `count`       | int    | URL               | Yes       |

**Response Properties**

| Property      | Type   | Description                          |
| -----------   | ------ | ------------------------------------ |
| `type`        | string | The Accumulate object type           |
| `start`       | int    |                                      |
| `count`       | int    |                                      |
| `total`       | int    |                                      |


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

| Parameter     | Type   | Description       | Required? |
| ---------     | ------ | ----------------- | --------- |
| `url`         | string | URL               | Yes       |

**Response Properties**

| Property      | Type   | Description                          |
| -----------   | ------ | ------------------------------------ |
| `type`        | string | The Accumulate object type           |
| `start`       | int    |                                      |
| `count`       | int    |                                      |
| `total`       | int    |                                      |


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

| Property    | Type   | Description            |
| ----------- | ------ | -------------------    |
| `txid`      | string | The transasction ID    |
| `hash`      | string | Token Transaction      |
| `message`   | string | The success Message    |

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
| `key`     | string | hash of public key      | No        |

**Response Properties**

| Property  | Type   | Description                                |
| --------- | ------ | -------------------------------------------|
| `type` | string    | The Accumulate object type                 |
| `data` | object    | The data for this object (properties vary) |

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

| Parameter     | Type   | Description                                  | Required? |
| ------------- | ------ | ---------------------------------------------| --------- |
| `origin`      | string | The origin account                           | Yes       |
| `sponsor`     | string | The data for this object (properties vary)   | Yes       |
| `signer`      | object | ADI signing  this request                    | Yes       |
| `signature`   | string | Signature of the ADI signing the transaction | Yes       |
| `keyPage`     | object | The keypage for this object                  | Yes       |
| `payload`     | object | The data for this object (properties vary)   | Yes       |


**Response Properties**

| Property    | Type   | Description            |
| ----------- | ------ | -------------------    |
| `hash`      | string | Token Transaction      |
| `txid`      | string | The transasction ID    |
| `message`   | string | The success Message    |


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
        "hash": "0905fa3ec38600bef28005f09971c615cc6f9d4a30f6e16949c47fde21652eb1",
        "message": "CheckTx",
        "txid": "24aea6af366f2560cdebcf91dfc3e7518eb0b01c04edbbbac16569c5b765622f"
    },
    "id": 0
}
```

### create-data-account

Creates a new data account under an ADI

**Request Parameters**

| Parameter     | Type   | Description                                  | Required? |
| ------------- | ------ | ---------------------------------------------| --------- |
| `origin`      | string | The origin account                           | Yes       |
| `sponsor`     | string | The data for this object (properties vary)   | Yes       |
| `signer`      | object | ADI signing  this request                    | Yes       |
| `signature`   | string | Signature of the ADI signing the transaction | Yes       |
| `keyPage`     | object | The keypage for this object                  | Yes       |
| `payload`     | object | The data for this object (properties vary)   | Yes       |


**Response Properties**

| Property    | Type   | Description            |
| ----------- | ------ | -------------------    |
| `hash`      | string | Token Transaction      |
| `txid`      | string | The transasction ID    |
| `message`   | string | The success Message    |

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
        "hash": "d81f710a70689fa3a42fdb3662555987ef260a17a426ef6e7760649e2219d2e5",
        "message": "CheckTx",
        "txid": "77b2d61f2e6a5c9da8cadf57dd8bdd57ec0846930630270a7fa32ea4e177d879"
    },
    "id": 0
}
```

### create-token-account

Creates a new token account for an ADI

**Request Parameters**

| Parameter     | Type   | Description                                  | Required? |
| ------------- | ------ | ---------------------------------------------| --------- |
| `origin`      | string | The origin account                           | Yes       |
| `sponsor`     | string | The data for this object (properties vary)   | Yes       |
| `signer`      | object | ADI signing  this request                    | Yes       |
| `signature`   | string | Signature of the ADI signing the transaction | Yes       |
| `keyPage`     | object | The keypage for this object                  | Yes       |
| `payload`     | object | The data for this object (properties vary)   | Yes       |


**Response Properties**

| Property    | Type   | Description            |
| ----------- | ------ | -------------------    |
| `hash`      | string | Token Transaction      |
| `txid`      | string | The transasction ID    |
| `message`   | string | The success Message    |

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

| Parameter     | Type   | Description                                  | Required? |
| ------------- | ------ | ---------------------------------------------| --------- |
| `origin`      | string | The origin account                           | Yes       |
| `sponsor`     | string | The data for this object (properties vary)   | Yes       |
| `signer`      | object | ADI signing  this request                    | Yes       |
| `signature`   | string | Signature of the ADI signing the transaction | Yes       |
| `keyPage`     | object | The keypage for this object                  | Yes       |
| `payload`     | object | The data for this object (properties vary)   | Yes       |


**Response Properties**

| Property    | Type   | Description            |
| ----------- | ------ | -------------------    |
| `hash`      | string | Token Transaction      |
| `txid`      | string | The transasction ID    |
| `message`   | string | The success Message    |

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
        "hash": "5b01c887701cbea996be9a2c199f815e57819d20a2ff4242fb3a7682190ec788",
        "message": "CheckTx",
        "txid": "dd70b0b3936f93651ae69776654d0de804a50040e2b6f023529264ff1fe6d414"
    },
    "id": 0
}
```

### update-key-page

Update key in a key page with a new public key

**Request Parameters**

| Parameter     | Type   | Description                                  | Required? |
| ------------- | ------ | ---------------------------------------------| --------- |
| `origin`      | string | The origin account                           | Yes       |
| `sponsor`     | string | The data for this object (properties vary)   | Yes       |
| `signer`      | object | ADI signing  this request                    | Yes       |
| `signature`   | string | Signature of the ADI signing the transaction | Yes       |
| `keyPage`     | object | The keypage for this object                  | Yes       |
| `payload`     | object | The data for this object (properties vary)   | Yes       |


**Response Properties**

| Property             | Type   | Description            |
| -----------------    | ------ | -------------------    |
| `transactionHash`    | string |  Transaction Hash      |
| `txid`               | string |  Transaction ID        |
| `envelopeHash`       | string |  Envelope Hash         |
| `simpleHash`         | string |  Simple Hash           |
| `hash`               | string |  Token Transaction     |

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

| Parameter     | Type   | Description                                  | Required? |
| ------------- | ------ | ---------------------------------------------| --------- |
| `origin`      | string | The origin account                           | Yes       |
| `sponsor`     | string | The data for this object (properties vary)   | Yes       |
| `signer`      | object | ADI signing  this request                    | Yes       |
| `signature`   | string | Signature of the ADI signing the transaction | Yes       |
| `keyPage`     | object | The keypage for this object                  | Yes       |
| `payload`     | object | The data for this object (properties vary)   | Yes       |


**Response Properties**

| Property    | Type   | Description            |
| ----------- | ------ | -------------------    |
| `hash`      | string | Token Transaction      |
| `txid`      | string | The transasction ID    |
| `message`   | string | The success Message    |

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
        "hash": "0905fa3ec38600bef28005f09971c615cc6f9d4a30f6e16949c47fde21652eb1",
        "message": "CheckTx",
        "txid": "24aea6af366f2560cdebcf91dfc3e7518eb0b01c04edbbbac16569c5b765622f"
    },
    "id": 0
}
```

### write-data

Write entry to a data account

**Request Parameters**

| Parameter     | Type   | Description                                  | Required? |
| ------------- | ------ | ---------------------------------------------| --------- |
| `origin`      | string | The origin account                           | Yes       |
| `sponsor`     | string | The data for this object (properties vary)   | Yes       |
| `signer`      | object | ADI signing  this request                    | Yes       |
| `signature`   | string | Signature of the ADI signing the transaction | Yes       |
| `keyPage`     | object | The keypage for this object                  | Yes       |
| `payload`     | object | The data for this object (properties vary)   | Yes       |


**Response Properties**

| Property             | Type   | Description            |
| -----------------    | ------ | -------------------    |
| `transactionHash`    | string |  Transaction Hash      |
| `txid`               | string |  Transaction ID        |
| `envelopeHash`       | string |  Envelope Hash         |
| `simpleHash`         | string |  Simple Hash           |
| `hash`               | string |  Token Transaction     |

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

| Parameter     | Type   | Description                                  | Required? |
| ------------- | ------ | ---------------------------------------------| --------- |
| `origin`      | string | The origin account                           | Yes       |
| `sponsor`     | string | The data for this object (properties vary)   | Yes       |
| `signer`      | object | ADI signing  this request                    | Yes       |
| `signature`   | string | Signature of the ADI signing the transaction | Yes       |
| `keyPage`     | object | The keypage for this object                  | Yes       |
| `payload`     | object | The data for this object (properties vary)   | Yes       |


**Response Properties**

| Property    | Type   | Description            |
| ----------- | ------ | -------------------    |
| `hash`      | string | Token Transaction      |
| `txid`      | string | The transasction ID    |
| `message`   | string | The success Message    |

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

| Parameter     | Type   | Description                                  | Required? |
| ------------- | ------ | ---------------------------------------------| --------- |
| `origin`      | string | The origin account                           | Yes       |
| `sponsor`     | string | The data for this object (properties vary)   | Yes       |
| `signer`      | object | ADI signing  this request                    | Yes       |
| `signature`   | string | Signature of the ADI signing the transaction | Yes       |
| `keyPage`     | object | The keypage for this object                  | Yes       |
| `payload`     | object | The data for this object (properties vary)   | Yes       |


**Response Properties**

| Property             | Type   | Description            |
| -----------------    | ------ | -------------------    |
| `transactionHash`    | string |  Transaction Hash      |
| `txid`               | string |  Transaction ID        |
| `envelopeHash`       | string |  Envelope Hash         |
| `simpleHash`         | string |  Simple Hash           |
| `hash`               | string |  Token Transaction     |

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

| Parameter     | Type   | Description                                  | Required? |
| ------------- | ------ | ---------------------------------------------| --------- |
| `origin`      | string | The origin account                           | Yes       |
| `sponsor`     | string | The data for this object (properties vary)   | Yes       |
| `signer`      | object | ADI signing  this request                    | Yes       |
| `signature`   | string | Signature of the ADI signing the transaction | Yes       |
| `keyPage`     | object | The keypage for this object                  | Yes       |
| `payload`     | object | The data for this object (properties vary)   | Yes       |


**Response Properties**

| Property             | Type   | Description            |
| -----------------    | ------ | -------------------    |
| `transactionHash`    | string |  Transaction Hash      |
| `txid`               | string |  Transaction ID        |
| `envelopeHash`       | string |  Envelope Hash         |
| `simpleHash`         | string |  Simple Hash           |
| `hash`               | string |  Token Transaction     |

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

| Parameter     | Type   | Description                                  | Required? |
| ------------- | ------ | ---------------------------------------------| --------- |
| `origin`      | string | The origin account                           | Yes       |
| `sponsor`     | string | The data for this object (properties vary)   | Yes       |
| `signer`      | object | ADI signing  this request                    | Yes       |
| `signature`   | string | Signature of the ADI signing the transaction | Yes       |
| `keyPage`     | object | The keypage for this object                  | Yes       |
| `payload`     | object | The data for this object (properties vary)   | Yes       |


**Response Properties**

| Property             | Type   | Description            |
| -----------------    | ------ | -------------------    |
| `transactionHash`    | string |  Transaction Hash      |
| `txid`               | string |  Transaction ID        |
| `envelopeHash`       | string |  Envelope Hash         |
| `simpleHash`         | string |  Simple Hash           |
| `hash`               | string |  Token Transaction     |

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

| Parameter     | Type   | Description                                  | Required? |
| ------------- | ------ | ---------------------------------------------| --------- |
| `origin`      | string | The origin account                           | Yes       |
| `sponsor`     | string | The data for this object (properties vary)   | Yes       |
| `signer`      | object | ADI signing  this request                    | Yes       |
| `signature`   | string | Signature of the ADI signing the transaction | Yes       |
| `keyPage`     | object | The keypage for this object                  | Yes       |
| `payload`     | object | The data for this object (properties vary)   | Yes       |


**Response Properties**

| Property    | Type   | Description            |
| ----------- | ------ | -------------------    |
| `hash`      | string | Token Transaction      |
| `txid`      | string | The transasction ID    |
| `message`   | string | The success Message    |

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

| Parameter     | Type   | Description                                  | Required? |
| ------------- | ------ | ---------------------------------------------| --------- |
| `origin`      | string | The origin account                           | Yes       |
| `sponsor`     | string | The data for this object (properties vary)   | Yes       |
| `signer`      | object | ADI signing  this request                    | Yes       |
| `signature`   | string | Signature of the ADI signing the transaction | Yes       |
| `keyPage`     | object | The keypage for this object                  | Yes       |
| `payload`     | object | The data for this object (properties vary)   | Yes       |


**Response Properties**

| Property    | Type   | Description            |
| ----------- | ------ | -------------------    |
| `hash`      | string | Token Transaction      |
| `txid`      | string | The transasction ID    |
| `message`   | string | The success Message    |

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