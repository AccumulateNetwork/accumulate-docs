# API Reference

### Format

This API uses the JSON-RPC 2.0 format. For more information on making JSON-RPC calls, see [Issuing API Calls](issuing-api-calls.md#json-rpc-formatted-apis).

### Endpoint

`[node-ip]:[http-port]/v1`

#### Testnet Endpoint

`https://testnet.accumulatenetwork.io/v1`

## Methods

**URL methods**

### get

Returns Accumulate Object by URL

#### Request Parameters

| Parameter | Type | Description | Required? |
| --------- | ---- | ----------- | --------- |
| `tbd`     | tbd  |             |           |

#### Response Properties

| Property | Type | Description |
| -------- | ---- | ----------- |
| `tbd`    | tbd  |             |

#### Errors

| Code | Message |
| ---- | ------- |
|      |         |

#### Example Request

```d
```

#### Example Response

```d
```

###

## ADI methods

### adi

Get ADI (Accumulate Digital Identity) info

#### Request Parameters

| Parameter | Type   | Description          | Required? |
| --------- | ------ | -------------------- | --------- |
| url       | string | The ADI URL to check | Yes       |

#### Response Properties

| Property        | Type   | Description                                     |
| --------------- | ------ | ----------------------------------------------- |
| `url`           | string | The URL for this ADI                            |
| `publicKeyHash` | string | The SHA-256 hash of the Public Key for this ADI |

#### Errors

| Code   | Message            |
| ------ | ------------------ |
| -32901 | Invalid ADI URL    |
| -32902 | ADI does not exist |

#### Example Request

```d
curl -X POST --data '{
    "jsonrpc": "2.0",
    "id": 0,
    "method": "adi",
    "params": {
        "url": "redwagon"
    }
}' -H 'content-type:application/json;' 127.0.0.1:35554/v1
```

#### Example Response

```d
{
    "jsonrpc": "2.0",
    "result": {
        "url": "redwagon",
        "publicKeyHash": "2ed111975d438e64bd2eb455be285b186e5ebd525d45dd8c274dff30edb59",
    },
    "id": 0
}
```

###

### adi-create

Create a new ADI (Accumulate Digital Identity)

#### Request Parameters

| Parameter   | Type   | Description                                  | Required? |
| ----------- | ------ | -------------------------------------------- | --------- |
| `adi`       | object | The ADI to create                            | Yes       |
| `signer`    | object | Existing ADI signing this request            | Yes       |
| `timestamp` | object | UNIX timestamp                               | Yes       |
| `sig`       | string | Signature of the ADI signing the transaction | Yes       |

#### Response Properties

| Property | Type   | Description     |
| -------- | ------ | --------------- |
| ADI      | object | The created ADI |

#### Errors

| Code   | Message            |
| ------ | ------------------ |
| -32901 | Invalid ADI URL    |
| -32801 | Invalid signer ADI |
| -32802 | Invalid signature  |
| -32803 | Invalid timestamp  |

#### Example Request

```cpp
curl -X POST --data '{
    "jsonrpc": "2.0",
    "id": 0,
    "method": "adi-create",
    "params": {
        "adi": {
            "url": "quantumfield",
            "publicKeyHash": "1403D9DB8AC1556C24065D9F1A946DE46A6F609B9476B9DE3C9FAFE6254F2",
        },
        "signer": {
            "url": "redwagon",
            "publicKey": "2ed111975d438e64bd2eb455be285b186e5ebd525d45dd8c274dff30edb59"
        },
        "timestamp": 1631306251,
        "sig": "________________________"
    }
}' -H 'content-type:application/json;' 127.0.0.1:35554/v1
```

#### Example Response

```d
{
    "jsonrpc": "2.0",
    "result": {
        "adi": {
            "url": "quantumfield",
            "publicKeyHash": "1403D9DB8AC1556C24065D9F1A946DE46A6F609B9476B9DE3C9FAFE6254F2",
        }
    },
    "id": 0
}
```

###

## Token methods

### token

Get Token info

#### Request Parameters

| Parameter | Type   | Description | Required? |
| --------- | ------ | ----------- | --------- |
| `url`     | string | Token URL   | Yes       |

#### Response Properties

| Property | Type   | Description              |
| -------- | ------ | ------------------------ |
| `token`  | object | The requested token info |

#### Errors

| Code   | Message              |
| ------ | -------------------- |
| -33001 | Invalid token URL    |
| -33002 | Token does not exist |

#### Example Request

```cpp
curl -X POST --data '{
    "jsonrpc": "2.0",
    "id": 0,
    "method": "token",
    "params": {
        "url": "redwagon/WagonToken"
    }
}' -H 'content-type:application/json;' 127.0.0.1:35554/v1
```

#### Example Response

```d
{
    "jsonrpc": "2.0",
    "result": {
        "token": {
            "url": "redwagon/WagonToken",
            "symbol": "WT",
            "precision": 4
        }
    },
    "id": 0
}
```

###

### token-create

Create Token

#### Request Parameters

| Parameter   | Type    | Description                                  | Required? |
| ----------- | ------- | -------------------------------------------- | --------- |
| `token`     | object  | New token                                    | Yes       |
| `signer`    | object  | ADI signing the creation of new token        | Yes       |
| `timestamp` | integer | UNIX timestamp                               | Yes       |
| `sig`       | string  | Signature of the ADI signing the transaction | Yes       |

#### Response Properties

| Property | Type   | Description       |
| -------- | ------ | ----------------- |
| token    | object | The created token |

#### Errors

| Code   | Message            |
| ------ | ------------------ |
| -33001 | Invalid token URL  |
| -32801 | Invalid signer ADI |
| -32802 | Invalid signature  |
| -32803 | Invalid timestamp  |

#### Example Request

```cpp
curl -X POST --data '{
    "jsonrpc": "2.0",
    "id": 0,
    "method": "token-create",
    "params": {
        "token": {
            "url": "quantumfield/Qbits",
            "symbol": "QB",
            "precision": 18
        },
        "signer": {
            "url": "quantumfield",
            "publicKey": "1403D9DB8AC1556C24065D9F1A946DE46A6F609B9476B9DE3C9FAFE6254F2"
        },
        "timestamp": 1631306251,
        "sig": "_________________________"
    }
}' -H 'content-type:application/json;' 127.0.0.1:35554/v1
```

#### Example Response

```d
{
    "jsonrpc": "2.0",
    "result": {
        "token": {
            "url": "quantumfield/Qbits",
            "symbol": "QB",
            "precision": 18
        }
    },
    "id": 0
}
```

###

### token-account

Get Token Account info

#### Request Parameters

| Parameter | Type   | Description       | Required? |
| --------- | ------ | ----------------- | --------- |
| `url`     | string | Token Account URL | Yes       |

#### Response Properties

| Property                  | Type   | Description                |
| ------------------------- | ------ | -------------------------- |
| `tokenAccountWithBalance` | object | Token account with balance |

#### Errors

| Code   | Message                      |
| ------ | ---------------------------- |
| -34001 | Invalid token account URL    |
| -34002 | Token account does not exist |

#### Example Request

```cpp
curl -X POST --data '{
    "jsonrpc": "2.0",
    "id": 0,
    "method": "token-account",
    "params": {
        "url": "quantumfield"
    }
}' -H 'content-type:application/json;' 127.0.0.1:35554/v1
```

#### Example Response

```d
{
    "jsonrpc": "2.0",
    "result": {
        "tokenAccountWithBalance": {
            "url": "quantumfield",
            "tokenURL": "quantumfield/QBits",
            "balance": 10000000000000
        }
    },
    "id": 0
}
```

###

### token-account-create

Create Token Account

#### Request Parameters

| Parameter      | Type    | Description                                   | Required? |
| -------------- | ------- | --------------------------------------------- | --------- |
| `tokenAccount` | object  | New token account                             | Yes       |
| `signer`       | object  | ADI signing the creation of new Token Account | Yes       |
| `timestamp`    | integer | UNIX timestamp                                | Yes       |
| `sig`          | string  | Signature of the ADI signing the transaction  | Yes       |

#### Response Properties

| Property       | Type   | Description   |
| -------------- | ------ | ------------- |
| `tokenAccount` | object | Token account |

#### Errors

| Code   | Message                   |
| ------ | ------------------------- |
| -34001 | Invalid token account URL |
| -33001 | Invalid token URL         |
| -32801 | Invalid signer ADI        |
| -32802 | Invalid signature         |
| -32803 | Invalid timestamp         |

#### Example Request

```cpp
curl -X POST --data '{
    "jsonrpc": "2.0",
    "id": 0,
    "method": "token-account-create",
    "params": {
        "tokenAccount": {
            "url": "redwagon",
            "tokenURL": "redwagon/WagonCoin"
        },
        "signer": {
            "url": "redwagon",
            "publicKey": "2ed111975d438e64bd2eb455be285b186e5ebd525d45dd8c274dff30edb59"
        },
        "timestamp": 1631306251,
        "sig": "____________"
    }
}' -H 'content-type:application/json;' 127.0.0.1:35554/v1
```

#### Example Response

```d
{
    "jsonrpc": "2.0",
    "result": {
        "tokenAccount": {
            "url": "redwagon",
            "tokenURL": "redwagon/WagonCoin"
        }
    },
    "id": 0
}
```

###

### token-tx

Get Token Transaction info

#### Request Parameters

| Parameter | Type   | Description      | Required? |
| --------- | ------ | ---------------- | --------- |
| `hash`    | string | Transaction hash | Yes       |

#### Response Properties

| Property          | Type   | Description       |
| ----------------- | ------ | ----------------- |
| `tokenTxWithHash` | object | Token transaction |

#### Errors

| Code   | Message                    |
| ------ | -------------------------- |
| -34002 | Invalid transaction hash   |
| -34003 | Transaction does not exist |

#### Example Request

```cpp
curl -X POST --data '{
    "jsonrpc": "2.0",
    "id": 0,
    "method": "token-tx",
    "params": {
        "hash": "f1d6daf52c3256b917405d465572e59c248b2db135e5d714e0ac5c43760ce434"
    }
}' -H 'content-type:application/json;' 127.0.0.1:35554/v1
```

#### Example Response

```d
{
    "jsonrpc": "2.0",
    "result": {
        "tokenTxWithHash": {
            "hash": "f1d6daf52c3256b917405d465572e59c248b2db135e5d714e0ac5c43760ce434",
            "from": "quantumfield",
            "to": [
                {
                    "url": "redwagon",
                    "amount": 500,
                },
                {
                    "url": "rhaegartargaryen",
                    "amount": 283
                }
            ],
            "meta": "Prince Rhaegar Targaryen was the firstborn son of King Aerys II Targaryen and his sister-wife, Queen Rhaella"
        }
    },
    "id": 0
}
```

###

### token-tx-create

Create Token Transaction

#### Request Parameters

| Parameter   | Type    | Description                                  | Required? |
| ----------- | ------- | -------------------------------------------- | --------- |
| `tokenTx`   | object  | New token transaction                        | Yes       |
| `signer`    | object  | ADI signing the transaction                  | Yes       |
| `timestamp` | integer | UNIX timestamp                               | Yes       |
| `sig`       | string  | Signature of the ADI signing the transaction | Yes       |

#### Response Properties

| Property          | Type   | Description       |
| ----------------- | ------ | ----------------- |
| `tokenTxWithHash` | object | Token transaction |

#### Errors

| Code   | Message                   |
| ------ | ------------------------- |
| -34001 | Invalid token address URL |
| -32801 | Invalid signer ADI        |
| -32802 | Invalid signature         |
| -32803 | Invalid timestamp         |

#### Example Request

```cpp
curl -X POST --data '{
    "jsonrpc": "2.0",
    "id": 0,
    "method": "____",
    "params": {}
}' -H 'content-type:application/json;' 127.0.0.1:35554/v1
```

#### Example Response

```d
{
    "jsonrpc": "2.0",
    "result": {
        "___": {}
    },
    "id": 0
}
```

### faucet

Get free ACME tokens

#### Request Parameters

| Parameter | Type | Description | Required? |
| --------- | ---- | ----------- | --------- |
|           |      |             |           |

#### Response Properties

| Property | Type | Description |
| -------- | ---- | ----------- |
|          |      |             |

#### Errors

| Code | Message |
| ---- | ------- |
|      |         |
|      | ​       |

#### Example Request

```cpp
```

#### Example Response

```d
```

####

## Key management methods
