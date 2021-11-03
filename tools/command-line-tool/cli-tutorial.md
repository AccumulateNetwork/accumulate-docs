# CLI Tutorial

The following tutorial will help you get started with the CLI tool and understand how it works. We'll run through a few basic commands to create and fund an account, and send tokens between the two.

{% hint style="warning" %}
This tutorial assumes you have already built the executable for the CLI tool. If you have not yet done so, visit [using-the-command-line.md] to learn how.
{% endhint %}

### Creating an anonymous token account

The first step is to create an anonymous token account using the `account generate` command. This command will create an account URL and corresponding private key, which will be stored locally on your computer. Since this command only generates an account locally, we don't need to worry about connecting to a node.

```bash
$ ./cli account generate
```

Remember that if you are on Windows you must use `./cli.exe` instead.

Once you run the command, you should get an output with the address for your token account. It will look something like: `acc://8c2bd7278f932663fcba7053f86d0b23e178913e9479c5ad/ACME`.

### Funding your account

Right now the account we created only exists locally, and therefore you won't be able to query the address in a block explorer or through the `get` command in the CLI. We must first complete a transaction using this account in order for it to be broadcast to the network. Let's fund our new account using the `faucet` command, which will both broadcast the existence of our new account, and give us some free tokens.

Since this command actually requires broadcasting to the network, we need to make sure we are connected to a node. We do that with the `-s` flag, followed by the server address for the node we want to connect to.

{% hint style="info" %}
_Note_: If you're running your own node locally, you don't need to specify the server with `-s`. The CLI will connect to your local node by default.
{% endhint %}

You can find a list of the available servers in the [Networks.go file](https://github.com/AccumulateNetwork/accumulated/blob/develop/networks/networks.go). For this tutorial we'll use `https://testnet.accumulatenetwork.io/v1`.

```bash
$ ./cli faucet <your account address> -s https://testnet.accumulatenetwork.io/v1
```

### Checking your account balance

Now that we've ran the `faucet` command, the network should know that our account exists. Let's check our account balance to see how many tokens we got from the faucet. We can do that with the `account get` command (remember to use the `-s` flag if you are not running a node locally).

```bash
$ ./cli account get <your account address> -s https://testnet.accumulatenetwork.io/v1
```

We should get an output that looks something like this:

```json
{
  "data": {
    "balance": "1000000000",
    "creditBalance": "0",
    "keyBookUrl": "",
    "nonce": 0,
    "tokenUrl": "acc://ACME",
    "txCount": 2,
    "url": "acc://your-account/ACME"
  },
  "keyPage": null,
  "mdRoot": "0000000000000000000000000000000000000000000000000000000000000000",
  "sponsor": "",
  "type": "anonTokenAccount"
}
```

Looking at the above, we can see under `"balance"` that we have `1000000000`, which is equivalent to 10 ACME tokens.

### Sending tokens

Now let's try sending some ACME tokens from one account to the other. We can use the account we already funded as the sending account. We'll have to create another account for the receiving account, so do that with `account generate`.

To send tokens, we'll need to use the `tx create` command. Once you have your sending and receiving accounts ready, run the command, followed by the account address for the sending account, then the account address for the receiving account, and finally the amount you want to send (and don't forget the `-s` flag if you're not running your own node).

{% hint style="info" %}
_Note_: The unit size for ACME balances in the CLI is 1/100,000,000. So if you want to send 1 ACME token, you'll need to enter 100000000 as the amount.
{% endhint %}

```bash
$ ./cli tx create <sending account> <receiving account> <amount to send> -s https://testnet.accumulatenetwork.io/v1
```

We should receive a response that looks like this:

```json
{
  "data": {
    "codespace": "",
    "hash": "70DAAF2DA6373FE2DB8248FE743BB87D595B58CD61F7DAB8F44AFC6CF825169C",
    "txid": "28f01f719ce177e004bfb875c9c0c5c29a166b61cf2ec8c024f3686b6bb4ae56"
  },
  "keyPage": null,
  "sponsor": "",
  "type": "tokenTx"
}
```

### Checking transaction info

Finally, let's make sure that the transaction was successfully broadcast. This time we will us the `tx get` command, and we'll pass in the transaction id (`"txid"`) that we received in the response output when we ran `tx create`.

```bash
$ ./cli tx get <txid> -s https://testnet.accumulatenetwork.io/v1
```

If the transaction was successful, the response we receive should look something like this:

```json
{
  "data": {
    "from": "acc://8c2bd7278f932663fcba7053f86d0b23e178913e9479c5ad/ACME",
    "to": [
      {
        "amount": 78934,
        "txid": "0d98a9c05cfcc9885705a71dbf1165ad4718c10bb86c191ed181ab3aabb6a534",
        "url": "acc://ba61c4d7dced236b9f89c908664bb7d80868097a363a6461/ACME"
      }
    ],
    "txid": "28f01f719ce177e004bfb875c9c0c5c29a166b61cf2ec8c024f3686b6bb4ae56"
  },
  "keyPage": {
    "height": 1,
    "index": 0
  },
  "sig": "232f4f34c358ea9c67908bb9e02608565233425efec44e4be7aa7f518aff3e0542fcbe8d807bee00530d3f448bdfd2780e09471263fe81434397ee5f956deb0c",
  "signer": {
    "nonce": 1635897963,
    "publicKey": "60358024268e1c7ba68d1d0b246ae3083d62ae4f27a2aaeb65695faef08d3ad5"
  },
  "sponsor": "acc://8c2bd7278f932663fcba7053f86d0b23e178913e9479c5ad/ACME",
  "status": {
    "code": "0"
  },
  "type": "tokenTx"
}
```


### The end

That's all for this tutorial, but you can find more commands and examples in the [Reference Guide](command-line-wallet.md).
