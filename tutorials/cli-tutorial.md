
# CLI Tutorial

The following tutorial will help you get started with the CLI tool and understand how it works. We'll run through a few basic commands to create and fund an account, and send tokens between the two.

{% hint style="warning" %}
This tutorial assumes you have already built the executable for the CLI tool. If you have not yet done so, visit [CLI Setup](../tools/command-line-tool/using-the-command-line.md) to learn how.
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

```bash
        Account Url     :       acc://5a48d2999da25641db06a8e4baf54a275bfc6ed90cbcd21a/ACME
        Token Url       :       acc://ACME
        Balance         :       10 ACME
        Credits         :       0
        Nonce           :       0
```

Looking at the above, we can see under `"balance"` that is 10 ACME tokens.

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

```bash
        Transaction Identifier  :       4a34fbf2efb1e374890dda349af8e106e4af4f7b38f4944bb2cd412d17a9d30f
        Tendermint Reference    :       b35694f3cf40ab1e61fbb69fc0a9a94f8c5f6a6e83f3ee54ff54366729fdce7f
        Error code              :       ok
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

### How to Create ADI

The following section deals will creating keypage and Accumulate Digital Identifier (ADI).

#### Create and list keypage

Prior to creating an ADI, you need to create a key which will be required as a parameter for ADI creation.

```bash
$ ./cli.exe key generate <keyname>
```

The output is displayed as

```bash
<keyname> : 20bb303068330cc761c35bb6425d269c7b4462c0daf78dc7dd15bcb51b496e05
```

You can see the list of key using

```bash
$ ./cli.exe key list
```

The output is displayed as

```bash
Public Key                                                              Key name
e086e27ff0bb5b146b6bdf55c8273211ddb62c684923502e22ef9d2d8b9a9ad5        <key name>
20bb303068330cc761c35bb6425d269c7b4462c0daf78dc7dd15bcb51b496e05        <key name>
```

#### Create new ADI using lite accounts

Now you can create an ADI using lite/annonymous account which was earlier described in the tutorial. The other parameters are the key name which was created just now, and name of the new ADI.

```bash
$ ./cli.exe  -s https://testnet.accumulatenetwork.io/v1 adi create <lite-account-address> <new-adi-name> <key name>
```

If the transaction was successful, the response we receive should look something like this:

```bash
        Transaction Identifier  :       1f3ce3f4f61b1b1b5b2a0b0436ffd22dc549eb222df84b4b6941de5087aab5a5
        Tendermint Reference    :       d7e3eddfbcd56c6f7c4635dddaa84b3a8f788da522ab8fa927b8ff6c2c02b98c
        Error code              :       ok
```

#### Create new ADI for another ADI

You can also create an ADI using another ADI and keypage as shown below:

```bash
$ ./cli.exe  -s https://testnet.accumulatenetwork.io/v1 adi create <existing-adi> <key name 1> <new-adi-name> <key name 2> 
```

If the transaction was successful, the response we receive should look something like this:

```bash
        Transaction Identifier  :       1074b68ae7c1ca4d1cf5f8f87f84cc4eb08ac916719b79547c9f5e1c451ff626
        Tendermint Reference    :       8b96ced206dd2252b00ee0b5e5e8814bd761f3cee1fb999dd0151aacf357c11c
        Error code              :       ok
```

### Checking the ADI accounts

You can check the ADI accounts using the following command:

```bash
$ ./cli.exe -s https://testnet.accumulatenetwork.io/v1 get <adi-name>
```

The Output should look something like:

```bash
        ADI Url         :       acc://xyzadi
        Key Book Url    :
```

### Account Create (ADI Token Account)

You can create a token account for an ADI

```bash
$ ./cli.exe  account create <adi-name> <wallet-key> <key index (optional)> <key height (optional)> <token account URL> <token URL> <keyBook (optional)>
```

The Output should look something like:

```bash
        Transaction Identifier  :       bcd5cc5fade48642082be7449b9d29208755c48365e79d181390375442dea6c3
        Tendermint Reference    :       011600eb026031530f06b48eabac9d575dc02e0e88ee300c28d25aaf9fd4d0e4
        Error code              :       ok
```

### Key Page Create

Create new key page with public key within the wallet

```bash
$ ./cli.exe -s https://testnet.accumulatenetwork.io/v1 page create <adi URL> <keyname> <new keypage URL> <keyname>
```
The Output should look something like:

```bash
{
   "​​""data":{
      "​​""codespace":"",
      "hash":"494832A75CE0F4995965ABC142C1ED7B2AD1A98167D828B30B9122777EA361E5",
      "txid":"d8072c4c1ebab505a9eea8298013606c4b77ac6fa3814596b05c2dc2d9d51912"
   }"​​",
   "keyPage":null,
   "sponsor":"",
   "txid":null,
   "type":"sigSpec"
}"​​"
```

### Get Key Page

You can get an existing Key Page by URL with the following command:

```bash
$ ./cli.exe page get <keypage URL>
```

The Output should look something like:

```bash
        Index   Nonce   Public Key                                                              Key Name
        0       0       ec52b1f5b263010912431bf8e4af6ed84b3b3d64baff41b306fec359a512e7b5
```

### Key Book Create

You can create a key book after creating a key page. Below is the command to create a keybook.

```bash
$ ./cli.exe book create <adi URL> <keyname> <new keybook URL> <existing keypage URL>
```
The Output should look something like:

```bash
2021/11/11 16:26:14
        Transaction Identifier  :       dd351321ca42568b9cc7e3a8faa88481e0e7e6759f4fd6b3976950b74865623a
        Tendermint Reference    :       71d231c0645a74c7ea21347bdcb54610e946f8a99eff0f48562634c14a928e27
        Error code              :       ok
```

### Get Key Book

You can get details of existing keybook URL with the following command:

```bash
$ ./cli.exe book get <keybook URL>
```
The Output should look something like:

```bash
        Height          Key Page Url
        1       :       acc://testadi1/keypage1
```

### How to send Credits

You can send credits using a lite account or adi key page to another lite account or adi key page.

```bash
$ ./cli.exe credits <lite account URL> <lite account or Key Page URL> <amount>
```
The Output should look something like:

```bash
        Transaction Identifier  :       81ddc13f2993f812bf41c895b5b485aeaf46095bc9695e0f30c49833e5f5450f
        Tendermint Reference    :       5fa567cef491714601b86f28bbdd0014130693a3e582fefeed9c1fb2886ece2b
        Error code              :       ok
```


### The end

That's all for this tutorial, but you can find more commands and examples in the [Reference Guide](broken-reference).
