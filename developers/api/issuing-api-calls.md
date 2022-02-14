---
description: This guide explains how to make calls to APIs exposed by Accumulate nodes.
---

# Issuing API Calls

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

The Accumulate API uses the [OpenRPC](https://open-rpc.org) specification for JSON-RPC 2.0 to describe its requests and responses.

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

####

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
