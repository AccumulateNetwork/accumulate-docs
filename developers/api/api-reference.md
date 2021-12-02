# API Reference

### Format

This API uses the JSON-RPC 2.0 format. For more information on making JSON-RPC calls, see [Issuing API Calls](issuing-api-calls.md#json-rpc-formatted-apis).

### Endpoint

`[node-ip]:[http-port]/v1`

#### Testnet Endpoint

`https://testnet.accumulatenetwork.io/v1`

## Methods

### _URL methods_

### get

Returns Accumulate Object by URL

**Request Parameters**

| Parameter | Type   | Description        | Required? |
| --------- | ------ | ------------------ | --------- |
| `url`     | string | Any Accumulate URL | Yes       |

**Response Properties**

| Property  | Type   | Description                                                                     |
| --------- | ------ | ------------------------------------------------------------------------------- |
| `type`    | string | The Accumulate object type                                                      |
| `mdRoot`  | string | The root hash of the patricia trie                                              |
| `data`    | object | The data for this object (properties vary)                                      |
| `sponsor` | string | The data for this object (properties vary)                                      |
| `keyPage` | TBD    | The [key page](../../deep-dive/key-management.md) within key book for this ADI. |

**Example Request**

```cpp
curl -X POST --data '{
    "jsonrpc": "2.0",
    "id": 0,
    "method": "get",
    "params": {
        "url": "acc://d4c8d9ab07daeecf50a7c78ff03c6524d941299e5601e578/ACME"
    }
}' -H 'content-type:application/json;' https://testnet.accumulatenetwork.io/v1
```

**Example Response**

```d
{
  "jsonrpc": "2.0",
  "result": {
    "type": "anonTokenAccount",
    "mdRoot": "0000000000000000000000000000000000000000000000000000000000000000",
    "data": {
      "url": "acc://d4c8d9ab07daeecf50a7c78ff03c6524d941299e5601e578/ACME",
      "tokenUrl": "acc://ACME",
      "keyBookUrl": "",
      "balance": "5000000000",
      "txCount": 5,
      "nonce": 0,
      "creditBalance": "0"
    },
    "sponsor": "",
    "keyPage": null
  },
  "id": 0
}
```

###

### _ADI methods_

### adi

Returns information about the specified ADI

**Request Parameters**

| Parameter | Type   | Description          | Required? |
| --------- | ------ | -------------------- | --------- |
| `url`     | string | The ADI URL to check | Yes       |

**Response Properties**

| Property        | Type   | Description                                     |
| --------------- | ------ | ----------------------------------------------- |
| `url`           | string | The URL for this ADI                            |
| `publicKeyHash` | string | The SHA-256 hash of the Public Key for this ADI |

**Errors**

| Code   | Message            |
| ------ | ------------------ |
| -32901 | Invalid ADI URL    |
| -32902 | ADI does not exist |

**Example Request**

```d
curl -X POST --data '{
    "jsonrpc": "2.0",
    "id": 0,
    "method": "adi",
    "params": {
        "url": "redwagon"
    }
}' -H 'content-type:application/json;' https://testnet.accumulatenetwork.io/v1
```

**Example Response**

```d
{
    "jsonrpc": "2.0",
    "result": {
        "type": "adi",
        "mdRoot": "0000000000000000000000000000000000000000000000000000000000000000",
        "data": {
            "url": "redwagon",
            "publicKey": "e086e27ff0bb5b146b6bdf55c8273211ddb62c684923502e22ef9d2d8b9a9ad5",
            "keyBookName": "",
            "keyPageName": ""
        },
        "sponsor": "",
        "keyPage": null,
        "txid": null
    },
    "id": 0
}
```

### _Token methods_

### token

Returns information about the specified token

**Request Parameters**

| Parameter | Type   | Description | Required? |
| --------- | ------ | ----------- | --------- |
| `url`     | string | Token URL   | Yes       |

**Response Properties**

| Property | Type   | Description              |
| -------- | ------ | ------------------------ |
| `token`  | object | The requested token info |

**Errors**

| Code   | Message              |
| ------ | -------------------- |
| -33001 | Invalid token URL    |
| -33002 | Token does not exist |

**Example Request**

```cpp
curl -X POST --data '{
    "jsonrpc": "2.0",
    "id": 0,
    "method": "token",
    "params": {
        "url": "acc://ACME"
    }
}' -H 'content-type:application/json;' https://testnet.accumulatenetwork.io/v1
```

**Example Response**

```d
{
    "jsonrpc": "2.0",
    "result": {
        "type": "token",
        "mdRoot": "0000000000000000000000000000000000000000000000000000000000000000",
        "data": {
            "url": "acc://ACME",
            "symbol": "ACME",
            "precision": 8,
            "propertiesUrl": ""
        },
        "sponsor": "",
        "keyPage": null,
        "txid": null
    },
    "id": 0
```

###

### token-account

Returns information about the specified token account

**Request Parameters**

| Parameter | Type   | Description       | Required? |
| --------- | ------ | ----------------- | --------- |
| `url`     | string | Token Account URL | Yes       |

**Response Properties**

| Property                  | Type   | Description                |
| ------------------------- | ------ | -------------------------- |
| `tokenAccountWithBalance` | object | Token account with balance |

**Errors**

| Code   | Message                      |
| ------ | ---------------------------- |
| -34001 | Invalid token account URL    |
| -34002 | Token account does not exist |

**Example Request**

```cpp
curl -X POST --data '{
    "jsonrpc": "2.0",
    "id": 0,
    "method": "token-account",
    "params": {
        "url": "acc://d4c8d9ab07daeecf50a7c78ff03c6524d941299e5601e578/ACME"
    }
}' -H 'content-type:application/json;' https://testnet.accumulatenetwork.io/v1
```

**Example Response**

```d
{
    "jsonrpc": "2.0",
    "result": {
        "type": "anonTokenAccount",
        "mdRoot": "0000000000000000000000000000000000000000000000000000000000000000",
        "data": {
            "url": "acc://d4c8d9ab07daeecf50a7c78ff03c6524d941299e5601e578/ACME",
            "tokenUrl": "acc://ACME",
            "keyBookUrl": "",
            "balance": "1000000000",
            "txCount": 1,
            "nonce": 0,
            "creditBalance": "0"
        },
        "sponsor": "",
        "keyPage": null
    },
    "id": 0
}
```

###

### token-account-history

Returns account history for the specified token account

**Request Parameters**

| Parameter | Type   | Description       | Required? |
| --------- | ------ | ----------------- | --------- |
| `url`     | string | Token Account URL | Yes       |

**Response Properties**

| Property          | Type   | Description       |
| ----------------- | ------ | ----------------- |
| `tokenTxWithHash` | object | Token transaction |

**Errors**

| Code   | Message                      |
| ------ | ---------------------------- |
| -34001 | Invalid token account URL    |
| -34002 | Token account does not exist |

**Example Request**

```cpp
curl -X POST --data '{
    "jsonrpc": "2.0",
    "id": 0,
    "method": "token-account-history",
    "params": {
        "url": "acc://53948aeb1cda7cf854c6ec3104a66e336d26be1ad1790bb7/ACME"
    }
}' -H 'content-type:application/json;' https://testnet.accumulatenetwork.io/v1
```

**Example Response**

```d
{
    "jsonrpc": "2.0",
    "result": {
        "data": [
            {
                "type": "syntheticTokenDeposit",
                "data": {
                    "txid": "ec183d7f1df5a5edc1e39369c7ab11094d0ae6898b5b66cff9ca2a18116b8b94",
                    "from": "acc://7117c50f04f1254d56b704dc05298912deeb25dbc1d26ef6/ACME",
                    "to": "acc://53948aeb1cda7cf854c6ec3104a66e336d26be1ad1790bb7/ACME",
                    "amount": "1000000000",
                    "tokenURL": "acc://ACME"
                },
                "sponsor": "acc://7117c50f04f1254d56b704dc05298912deeb25dbc1d26ef6/ACME",
                "keyPage": {
                    "height": 1,
                    "index": 0
                },
                "txid": "bda2bb7cc11b3944851623b245bc7816a8476f21c8e6bdde0786d6aa6d678010",
                "signer": {
                    "publicKey": "18fc600320f247cf71652cfb6125973defef1bfd9499f297e6172cb5b293e7e1",
                    "nonce": 37
                },
                "sig": "5cc19f7476688b97ab7c716019facaaf6d1179ea58b6d77046f1cc5ba94a79f54eaa0c7234968bc5db487d58b9384111bd6ba30de9e23aa10efd8e6a89a4800c",
                "status": {
                    "code": "0"
                }
            },
            {
                "type": "tokenTx",
                "data": {
                    "txid": "327912a9a0e9ef7916d358bc9cd5f4944adfdb168a2b017435e27a022c867ef7",
                    "from": "acc://53948aeb1cda7cf854c6ec3104a66e336d26be1ad1790bb7/ACME",
                    "to": [
                        {
                            "txid": "bbc37d5bae15363287faa72c4a3d663d9e2238ef7a07723de7ab3ec1ab7dc559",
                            "url": "acc://21f6a2751c8959919162dd9b9dd9306a574cb1035dcd229a/ACME",
                            "amount": 20000
                        }
                    ]
                },
                "sponsor": "acc://53948aeb1cda7cf854c6ec3104a66e336d26be1ad1790bb7/ACME",
                "keyPage": {
                    "height": 1,
                    "index": 0
                },
                "txid": "327912a9a0e9ef7916d358bc9cd5f4944adfdb168a2b017435e27a022c867ef7",
                "signer": {
                    "publicKey": "9d091adcb8426831b3a546be958c3d353521313182a75c9c76a642ef41fd4726",
                    "nonce": 1636285772
                },
                "sig": "5a1727a029f055c0cb3dceab2bd04a798b145bf4ea5c04ac54b9201b85f89428dcec2b549bd47daed9f1dafdefbea9cdfc64aeb6a81bec50482df8828287a10c",
                "status": {
                    "code": "0"
                }
            },
            {
                "type": "syntheticTokenDeposit",
                "data": {
                    "txid": "0fb8cc2eae7dbf26061fb2a0c6f6b3a3bd5754ebbdafa2fc4f933e1a5ad5cee8",
                    "from": "acc://7117c50f04f1254d56b704dc05298912deeb25dbc1d26ef6/ACME",
                    "to": "acc://53948aeb1cda7cf854c6ec3104a66e336d26be1ad1790bb7/ACME",
                    "amount": "1000000000",
                    "tokenURL": "acc://ACME"
                },
                "sponsor": "acc://7117c50f04f1254d56b704dc05298912deeb25dbc1d26ef6/ACME",
                "keyPage": {
                    "height": 431,
                    "index": 0
                },
                "txid": "f8ff5e4d0961d185db6dd3feb13be09371d84f7d8ae5f174357e5d76545ba1b4",
                "signer": {
                    "publicKey": "7408e7dc62924a98b6c24fa814eec2d40363f9769875613d4d5ee04fdc1db94a",
                    "nonce": 141
                },
                "sig": "7f8089d480644c50a269d40d8b1cf620bf75399ce54011ee8af95333b48c91ce31f3183b69854c326dad0b32af5e7ced662d72ac8a56a4b4cd1dfb830e2a650e",
                "status": {
                    "code": "0"
                }
            },
            {
                "type": "syntheticTokenDeposit",
                "data": {
                    "txid": "3fc71b785b7965fae89734ca4b4e4da253d592811e978fab06352aa171fc5bcb",
                    "from": "acc://7117c50f04f1254d56b704dc05298912deeb25dbc1d26ef6/ACME",
                    "to": "acc://53948aeb1cda7cf854c6ec3104a66e336d26be1ad1790bb7/ACME",
                    "amount": "1000000000",
                    "tokenURL": "acc://ACME"
                },
                "sponsor": "acc://7117c50f04f1254d56b704dc05298912deeb25dbc1d26ef6/ACME",
                "keyPage": {
                    "height": 433,
                    "index": 0
                },
                "txid": "f70df8cb52c06ce76bfc6b4f47348a8c671b34efedfc9d79bb1db1e130f581b0",
                "signer": {
                    "publicKey": "18fc600320f247cf71652cfb6125973defef1bfd9499f297e6172cb5b293e7e1",
                    "nonce": 142
                },
                "sig": "2dcec00259c6962f10ceaf142ae6b62352da7279b1ba6d3cfd264397a53d0cdd08b2de91ac4662c0a037009931acedb75b7ddce3f240088ce11a708d25a1eb08",
                "status": {
                    "code": "0"
                }
            }
        ],
        "type": "tokenAccountHistory",
        "start": 0,
        "limit": 20,
        "total": 4
    },
    "id": 0
}
```

###

### token-tx

Returns transaction data for the specified transaction

**Request Parameters**

| Parameter | Type   | Description      | Required? |
| --------- | ------ | ---------------- | --------- |
| `hash`    | string | Transaction hash | Yes       |

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
    "method": "token-tx",
    "params": {
        "hash": "327912a9a0e9ef7916d358bc9cd5f4944adfdb168a2b017435e27a022c867ef7"
    }
}' -H 'content-type:application/json;' https://testnet.accumulatenetwork.io/v1 get
```

**Example Response**

```d
{
    "jsonrpc": "2.0",
    "result": {
        "type": "tokenTx",
        "data": {
            "txid": "327912a9a0e9ef7916d358bc9cd5f4944adfdb168a2b017435e27a022c867ef7",
            "from": "acc://53948aeb1cda7cf854c6ec3104a66e336d26be1ad1790bb7/ACME",
            "to": [
                {
                    "txid": "bbc37d5bae15363287faa72c4a3d663d9e2238ef7a07723de7ab3ec1ab7dc559",
                    "url": "acc://21f6a2751c8959919162dd9b9dd9306a574cb1035dcd229a/ACME",
                    "amount": 20000
                }
            ]
        },
        "sponsor": "acc://53948aeb1cda7cf854c6ec3104a66e336d26be1ad1790bb7/ACME",
        "keyPage": {
            "height": 1,
            "index": 0
        },
        "txid": "327912a9a0e9ef7916d358bc9cd5f4944adfdb168a2b017435e27a022c867ef7",
        "signer": {
            "publicKey": "9d091adcb8426831b3a546be958c3d353521313182a75c9c76a642ef41fd4726",
            "nonce": 1636285772
        },
        "sig": "5a1727a029f055c0cb3dceab2bd04a798b145bf4ea5c04ac54b9201b85f89428dcec2b549bd47daed9f1dafdefbea9cdfc64aeb6a81bec50482df8828287a10c",
        "status": {
            "code": "0"
        }
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
| `codespace` | string |                     |

**Example Request**

```cpp
curl -X POST --data '{
    "jsonrpc": "2.0",
    "id": 0,
    "method": "faucet",
    "params": {
        "url": "acc://d4c8d9ab07daeecf50a7c78ff03c6524d941299e5601e578/ACME"
    }
}' -H 'content-type:application/json;' https://testnet.accumulatenetwork.io/v1
```

**Example Response**

```d
{
  "jsonrpc": "2.0",
  "result": {
    "type": "",
    "data": {
      "txid": "b1890c357977063b3088c444867253fb0ea7d5243a3e58ca8b8aa6b34a766765",
      "hash": "EDED8E9BC71463FF193E10863A59FEEDAF1355A1917608E715A6E9082E06B60D",
      "codespace": ""
    },
    "sponsor": "",
    "keyPage": null,
    "txid": null
  },
  "id": 0
}
```

### _Key management methods_

### keypage

Returns the specified key page / signature specification

{% hint style="info" %}
_**NOTE: Key page = ****`sig-spec`****. Method names will be updated soon.**_
{% endhint %}

**Request Parameters**

| Parameter | Type   | Description             | Required? |
| --------- | ------ | ----------------------- | --------- |
| `url`     | string | Accumulate Key Page URL | Yes       |

**Response Properties**

| Property  | Type   | Description                                                                                   |
| --------- | ------ | --------------------------------------------------------------------------------------------- |
| `keyPage` | object | An object containing the Chain URL, Key book ID, credit balance, and an unordered set of keys |

**Example Request**

```cpp
curl -X POST --data '{
    "jsonrpc": "2.0",
    "id": 0,
    "method": "sig-spec",
    "params": {
        "url": "acc://testadi1/keypage1"
    }
}' -H 'content-type:application/json;' https://testnet.accumulatenetwork.io/v1
```

**Example Response**

```d
{
    "jsonrpc": "2.0",
    "result": {
        "type": "sigSpec",
        "mdRoot": "0000000000000000000000000000000000000000000000000000000000000000",
        "data": {
            "type": 10,
            "url": "acc://testadi1/keypage1",
            "sigSpecId": "a0da002bf84abf1b88682be0131bc148201dcd38c360ed93a5e71d20408bf054",
            "creditBalance": 0,
            "keys": [
                {
                    "publicKey": "1c3681b851c1996b5768b2a7c16ea592d18b89286373c6f98e5414e0fb145c5f",
                    "nonce": 0
                }
            ]
        },
        "sponsor": "",
        "keyPage": null,
        "txid": null
    },
    "id": 0
}
```

###

### create-keypage

Creates a new key page (previously signature specification)

{% hint style="info" %}
_**NOTE: Key page = ****`sig-spec`****. Method names will be updated soon.**_
{% endhint %}

**Request Parameters**

| Parameter | Type    | Description                              | Required? |
| --------- | ------- | ---------------------------------------- | --------- |
| `wait`    | boolean | Wait for the transaction to be complete? | No        |
| `tx`      | object  | Transaction                              | Yes       |

**Response Properties**

| Property  | Type   | Description                |
| --------- | ------ | -------------------------- |
| `keyPage` | object | The newly created key page |

**Example Request**

```cpp
```

**Example Response**

```d
```

###

### keybook

Returns information about the specified key book / Signature specification group

{% hint style="info" %}
_**NOTE: Key book = ****`sig-spec-group`****. Method names will be updated soon.**_
{% endhint %}

**Request Parameters**

| Parameter | Type   | Description             | Required? |
| --------- | ------ | ----------------------- | --------- |
| `url`     | string | Accumulate key book URL | Yes       |

**Response Properties**

| Property  | Type   | Description                                      |
| --------- | ------ | ------------------------------------------------ |
| `keyBook` | object | Object containing the chain URL and key page IDs |

**Example Request**

```cpp
curl -X POST --data '{
    "jsonrpc": "2.0",
    "id": 0,
    "method": "sig-spec-group",
    "params": {
        "url": "acc://testadi1/keybook1"
    }
}' -H 'content-type:application/json;' https://testnet.accumulatenetwork.io/v1
```

**Example Response**

```d
{
    "jsonrpc": "2.0",
    "result": {
        "type": "sigSpecGroup",
        "mdRoot": "0000000000000000000000000000000000000000000000000000000000000000",
        "data": {
            "type": 11,
            "url": "acc://testadi1/keybook1",
            "sigSpecId": [
                0,
                0,
                0,
                0,
                0,
                0,
                0,
                0,
                0,
                0,
                0,
                0,
                0,
                0,
                0,
                0,
                0,
                0,
                0,
                0,
                0,
                0,
                0,
                0,
                0,
                0,
                0,
                0,
                0,
                0,
                0,
                0
            ],
            "sigSpecs": [
                "aabae67381f844ebe0cb59fa9ed73db8ad6f3e1e9d1d9332d784d0fb0344e09c"
            ]
        },
        "sponsor": "",
        "keyPage": null,
        "txid": null
    },
    "id": 0
}
```

###

### create-keybook

Creates a new key book / signature specification group

{% hint style="info" %}
_**NOTE: Key book = ****`sig-spec-group`****. Method names will be updated soon.**_
{% endhint %}

**Request Parameters**

| Parameter | Type    | Description                           | Required? |
| --------- | ------- | ------------------------------------- | --------- |
| `wait`    | boolean | Wait for the transaction to complete? | No        |
| `tx`      | object  | Transaction                           | Yes       |

**Response Properties**

| Property  | Type   | Description                |
| --------- | ------ | -------------------------- |
| `keyBook` | object | The newly created key book |

**Example Request**

```cpp
```

**Example Response**

```d
```

###

### update-key-page

Adds, removes, or updates a key in a key page

**Request Parameters**

| Parameter | Type    | Description                           | Required? |
| --------- | ------- | ------------------------------------- | --------- |
| `wait`    | boolean | Wait for the transaction to complete? | No        |
| `tx`      | Object  | Transaction                           | Yes       |

**Response Properties**

| Property | Type | Description |
| -------- | ---- | ----------- |
|          |      |             |

**Example Request**

```cpp
```

**Example Response**

```d
```

###

### _Credit methods_

### add-credits

Adds credits to a lite account or key page

**Request Parameters**

| Parameter | Type    | Description                           | Required? |
| --------- | ------- | ------------------------------------- | --------- |
| `wait`    | boolean | Wait for the transaction to complete? | No        |
| `tx`      | Object  | Transaction                           | Yes       |

**Response Properties**

| Property | Type | Description |
| -------- | ---- | ----------- |
|          |      |             |

**Errors**

| Code | Message |
| ---- | ------- |
|      |         |
|      | ​       |

**Example Request**

```cpp
```

**Example Response**

```d
```

###

### _Metrics_

### metrics - coming soon
