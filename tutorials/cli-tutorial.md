# CLI Tutorial

This tutorial will guide you in getting started with the CLI. We'll run through a few basic commands to create and fund an account, and send tokens between the two.

This tutorial assumes you have already built the executable for the CLI tool. If you have not yet done so, visit [CLI Setup](../tools/command-line-tool/using-the-command-line.md) for instructions on building the CLI.

### Creating a lite token account

The first step is to create a lite token account using the `account generate` command. This command will create an account URL and corresponding private key, which will be stored locally on your computer. Since this command only generates an account locally, it is not necessary to connect to a node, however, this also means that lite token account is not yet on the server.

```bash
$ ./cli account generate
```

Remember that if you are on Windows you must use `./cli.exe` instead.

Once you run the command, you should get an output with the address for your token account. It will look something like the following: `acc://d699fd22e466e7ea4f05a1f6b67fc67af555856f701bdf29/ACME : e258d215c12d610dad703482bc7c61a0f5db975fbfaf73c52f4533c5941b82d3`.

### Funding your account

The account that was created in the previous section currently only exist locally, and therefore you won't be able to query the address in a block explorer or through the `get` command in the CLI. We must first complete a transaction using this account in order for it to be broadcasted to the network. We will fund our new account using the `faucet` command, which will both broadcast the existence of our new account, and give us some free tokens.

Since this command actually requires broadcasting to the network, we need to make sure we are connected to a node. We do that with the `-s` flag, followed by the server address for the node we want to connect to.

{% hint style="info" %}
_Note_: If you're running your own node locally, you will need to specify your local server with `-s`.
{% endhint %}

You can find a list of the available servers in the [Networks.go file](https://github.com/AccumulateNetwork/accumulate/blob/develop/networks/networks.go). For this tutorial we'll use `https://testnet.accumulatenetwork.io/v1`.

```bash
$ ./cli faucet <your account address> -s https://testnet.accumulatenetwork.io/v1
```

This will return a statment similar to the following:

```bash
        Transaction Identifier  :       6dd7a8d90ffaa4d45ff5a538a06bdb6d13b3f3cf90763fae13797b4a935caed5
        Tendermint Reference    :       a0b30c13f68fbaf4ac3c943837dda06e912dc851f707f92f13e7894fabc9bd0a
        Error code              :       ok
```

### Checking your account balance

Now that we've ran the `faucet` command, the network will know that the account exists. Let's check the account balance to see how many tokens we have received from the faucet. We can do this with the `account get` command (remember to use the `-s` flag if you are not running a node locally).

```bash
$ ./cli account get <your account address> -s https://testnet.accumulatenetwork.io/v1
```

You should get an output that looks something like this:

```bash
        Account Url     :       acc://5a48d2999da25641db06a8e4baf54a275bfc6ed90cbcd21a/ACME
        Token Url       :       acc://ACME
        Balance         :       10 ACME
        Credits         :       0
        Nonce           :       0
```

Looking at the above, we can see under `"Balance"` that we have received 10 ACME tokens.

### Sending tokens

Now let's try sending some ACME tokens from one account to the other. You can use the account we already funded as the sending account. You'll need to create an additional account to receive the tokens. You will need to use the `account generate` again to establish the receiving account.

To send the tokens you will use the `tx create` command. Once you have the addresses of the sending and receiving accounts ready, run the command, followed by the account address for the sending account, then the account address for the receiving account, and finally the amount you would like to send (and don't forget the `-s` flag if you're not running your own node).

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

Finally, let's make sure that the transaction was successfully broadcast. This time you will use the `tx get` command, and we'll pass in the transaction id (`"txid"`) that we received in the response output from `tx create`.

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

## How to Create ADI

The following section deals will creating keypage and Accumulate Digital Identifier (ADI).

#### Create and list keypage

Prior to creating an ADI, you need to create a key which is one of the required parameters during the ADI creation process.

```bash
$ ./cli key generate <keyname>
```

The output is displayed as

```bash
<keyname> : 20bb303068330cc761c35bb6425d269c7b4462c0daf78dc7dd15bcb51b496e05
```

You can see the list of key using

```bash
$ ./cli key list
```

The output is displayed as

```bash
Public Key                                                              Key name
e086e27ff0bb5b146b6bdf55c8273211ddb62c684923502e22ef9d2d8b9a9ad5        <key name>
20bb303068330cc761c35bb6425d269c7b4462c0daf78dc7dd15bcb51b496e05        <key name>
```

#### Create new ADI using lite token accounts

Now you can create an ADI using one of your lite token accounts. The parameters of this function are the address of the lite account, the name you would like to assign to the ADI, and the name of the key.

```bash
$ ./cli  -s https://testnet.accumulatenetwork.io/v1 adi create <lite-token-account-address> <new-adi-name> <key name>
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
$ ./cli  -s https://testnet.accumulatenetwork.io/v1 adi create <existing-adi> <key name 1> <new-adi-name> <key name 2> 
```

If the transaction was successful, the response we receive should look something like this:

```bash
        Transaction Identifier  :       1074b68ae7c1ca4d1cf5f8f87f84cc4eb08ac916719b79547c9f5e1c451ff626
        Tendermint Reference    :       8b96ced206dd2252b00ee0b5e5e8814bd761f3cee1fb999dd0151aacf357c11c
        Error code              :       ok
```

### Checking the ADI accounts

You can view ADI accounts using the following command:

```bash
$ ./cli -s https://testnet.accumulatenetwork.io/v1 get <adi-name>
```

The Output should look something like:

```bash
{"data":{"keyBookName":"","keyPageName":"","publicKey":"0accaa51532dd9c0e955e7f3ec153befa4aa5e238943838c18ba9beaaa13064e","url":"acc://David"},
"keyPage":null,
"mdRoot":"0000000000000000000000000000000000000000000000000000000000000000",
"sponsor":"",
"txid":null,
"type":"adi"}
```

### Account Create (ADI Token Account)

You can create a token account for an ADI

```bash
$ ./cli  account create <adi-name> <wallet-key> <key index (optional)> <key height (optional)> <token account URL> <token URL> <keyBook (optional)>
```

The Output should look something like:

```bash
        Transaction Identifier  :       bcd5cc5fade48642082be7449b9d29208755c48365e79d181390375442dea6c3
        Tendermint Reference    :       011600eb026031530f06b48eabac9d575dc02e0e88ee300c28d25aaf9fd4d0e4
        Error code              :       ok
```

### Keypage Create

You can create new keypages with public key within the wallet

```bash
$ ./cli -s https://testnet.accumulatenetwork.io/v1 page create <adi URL> <keyname> <new keypage URL> <keyname>
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

### Get Keypage

You can get an existing Keypage by URL with the following command:

```bash
$ ./cli page get <keypage URL>
```

The Output should look something like:

```bash
        Index   Nonce   Public Key                                                              Key Name
        0       0       ec52b1f5b263010912431bf8e4af6ed84b3b3d64baff41b306fec359a512e7b5
```

### Keybook Create

You can create a keybook after creating a keypage. Below is the command to create a keybook.

```bash
$ ./cli book create <adi URL> <keyname> <new keybook URL> <existing keypage URL>
```

The Output should look something like:

```bash
2021/11/11 16:26:14
        Transaction Identifier  :       dd351321ca42568b9cc7e3a8faa88481e0e7e6759f4fd6b3976950b74865623a
        Tendermint Reference    :       71d231c0645a74c7ea21347bdcb54610e946f8a99eff0f48562634c14a928e27
        Error code              :       ok
```

### Get Keybook

You can get details of existing keybook URL with the following command:

```bash
$ ./cli book get <keybook URL>
```

The Output should look something like:

```bash
        Height          Key Page Url
        1       :       acc://testadi1/keypage1
```

### Keypage Hierarchy

In this section you will learn to create a keybook with multiple keypages and managing the keypages with hierarchy of keys that allow to participate in the execution of transactions. A Keybook is a prioritized list of Keypages, where the first page in the list is the highest priority and the last page is the lowest priority. The first keypage can modify any keypage, but the last keypage can only modify itself.

Below are the steps that you need to follow to generate keys, create ADI, add pages to the book and finally add/update keys:

#### Generate Keys

You create new keys or use existing keys. In this example new set of keys are created

```bash
$ ./cli key generate keytest-0-0
$ ./cli key generate keytest-1-0
$ ./cli key generate keytest-1-1
$ ./cli key generate keytest-2-0
$ ./cli key generate keytest-2-1
```

#### Create ADI

You can create an ADI using one of the key generated in the preious step and specifying the keybook and keypage name as parameters as shown below:

```bash
$ ./cli adi create <lite token account URL> keytestadi keytest-0-0 book page0
```

The Output should look something like:

```bash
        Transaction Identifier  :       c0ddc311cd19fb01bb1f05959191588f4507f288b1669973b91aa183a3063a7c
        Tendermint Reference    :       3f5b2a8af0e90c1ed1e3612a26b8612318de4587ea0b37cf7258005ebf02d646
        Error code              :       ok
```

#### Add keypages to the keybook

The next step is to add keypages to the keybook under the ADI which was created in the previous step. Below are the sample command and output:

```bash
$ ./cli page create keytestadi/book keytest-0-0 keytestadi/page1 keytest-1-0
```

```bash
{"data":{"codespace":"","hash":"87541A6483FF29779AB8528B9DA14BC5C747EB1F379D451AA76BF988E54B1777","txid":"81c2aa87078df1bcd368297a3f45a5324b27599c848b672650e6138ba1e4265e"},"keyPage":null,"sponsor":"","txid":null,"type":"sigSpec"}            :       ok
```

```bash
$ ./cli page create keytestadi/book keytest-0-0 keytestadi/page2 keytest-2-0
```

```bash
{"data":{"codespace":"","hash":"8A9B68686333AA64034FCFB1762DF4AA8DA7C12C9D9688B8DA9CA1F9A226E012","txid":"024d483ecfe44f1b8a76292ad6cd14847a3cec2a54866f3dc3e6f69620d32788"},"keyPage":null,"sponsor":"","txid":null,"type":"sigSpec"}           :       ok
```

#### Adding a key to page1 using a page1 key

You can add/modify a key to page1 using the key at the same priority level. You can try the below command to implement the same:

```bash
$ ./cli page key add keytestadi/page1 keytest-1-0 1 1 keytest-1-1
```

The Output should look something like:

```bash
        Transaction Identifier  :       f61b5344e863141f25d34c2f40d8d1e2bd4cd29687c5f98822f91e9e39500682
        Tendermint Reference    :       2572c943abfc91b7e2192d9522657f5fffc8f4da1df55d5d0807ebca6f67faf7
        Error code              :       ok
```

#### Adding a key to page2 using a page1 key

You can add/modify a key to page2 using the key at a higher priority level. You can try the below command to add a key to page2 using a page1 key:

```bash
$ ./cli page key add keytestadi/page2 keytest-1-0 1 1 keytest-2-1
```

The Output should look something like:

```bash
        Transaction Identifier  :       65dc57255960b0880dfccf5162bab0231ef1fb4b7ec09f72dc256ca9eec105b0
        Tendermint Reference    :       106d8eb1a87912ed94eff8a77a3e470f1cfc97a1e31d2223105e120e38a16869
        Error code              :       ok
```

#### Adding a key to page0 using a page1 key

You cannot add/modify a higher priority level page with a lower level key. Below is the command to attempt the same which throws an error.

```bash
$ ./cli page key add keytestadi/page0 keytest-1-0 1 1 keytest-1-1
```

The Output should throw error something like:

```bash
jsonrpc2.Error{Code:ErrorCode{-32603:"Internal error"}, Message:"Internal error"}
```

### How to send Credits

You can send credits using a lite token account or adi keypage to another lite token account or adi keypage.

```bash
$ ./cli credits <lite token account URL> <lite token account or Keypage URL> <amount>
```

The Output should look something like:

```bash
        Transaction Identifier  :       81ddc13f2993f812bf41c895b5b485aeaf46095bc9695e0f30c49833e5f5450f
        Tendermint Reference    :       5fa567cef491714601b86f28bbdd0014130693a3e582fefeed9c1fb2886ece2b
        Error code              :       ok
```

### The end

That is the end of this tutorial, but you can find more commands and examples in the [Reference Guide](broken-reference/).
