# Command Line Wallet

The Command-Line Interface Tool allows the following: token, identity, and key management. By default, the Command-Line Interface connects to a localhost Accumulate Node, but you can specify any remote server by using the flag.

### Basic commands and flags

```bash
Usage:
  accumulate [command] [flags]

Available Commands:
  account     Create and get token accounts
  adi         Create and manage ADI
  completion  generate the autocompletion script for the specified shell
  credits     Send credits to a recipient
  directory   Send credits to a recipient
  faucet      Get tokens from faucet
  get         Get data by URL
  help        Help about any command
  key         Create and manage Keys, Books, and Pages
  tx          Create and get token txs
  
Flags:
  -d, --debug              Print accumulated API calls
  -h, --help               help for accumulate
  -s, --server string      Accumulated server (default "http://localhost:35554/v1")
  -t, --timeout duration   Timeout for all API requests (i.e. 10s, 1m) (default 5s)
  
  Use "accumulate [command] --help" for more information about a command.
```

### Account

Anonymous token accounts are stored in a local database. CLI allows you to generate anon token accounts and export/import corresponding private keys.

```bash
  accumulate account get [url]                  Get anon token account by URL
  accumulate account generate                   Generate random anon token account
  accumulate account list                       Display all anon token accounts
  accumulate account create [{actor adi}] [wallet key label] [key index (optional)] [key height (optional)] [token account url] [tokenUrl] [keyBook (optional)]  Create a token account for an ADI
  accumulate account import [private-key]       Import anon token account from private key hex
  accumulate account export [url]               Export private key hex of anon token account
```

###

#### **Account generation**

```bash
> account generate
acc://3ed6b2003242d2166508e117a2a66f8ca742b72e8d90d736/ACME
```

#### Account export

```bash
> account export acc://3ed6b2003242d2166508e117a2a66f8ca742b72e8d90d736/ACME
22fe5656270db192406d33ac9c93aee611c361ce9380a514ab8be417e0be52778e5d0e715434e4105a8f57dda15fcb3bd235a55f85226d0ec5c1c733f9ed78fb
```

#### Account import

```bash
> account import 22fe5656270db192406d33ac9c93aee611c361ce9380a514ab8be417e0be52778e5d0e715434e4105a8f57dda15fcb3bd235a55f85226d0ec5c1c733f9ed78fb
acc://3ed6b2003242d2166508e117a2a66f8ca742b72e8d90d736/ACME
```

### Faucet

Faucet sends some testnet ACME tokens to requested anonymous token account.

```bash
Usage:
faucet [url]               Get tokens from faucet to address
```

Example of usage:

```bash
> accumulate faucet acc://3ed6b2003242d2166508e117a2a66f8ca742b72e8d90d736/ACME
{"data":{"codespace":"","hash":"C89966F8435FE6BC195DEB817CBCCBC3D9FF210EDA2B2B60F4CEC5E4E714F9A4","txid":"1d6138b453b7bee86f70e3012c2f0b4264dd631f6551965fe39b8bd1da08bb49"},"keyPage":null,"sponsor":"","type":""}
```

### Get

Get data by Accumulate URL.

```bash
Usage:
get [url]          Get data by Accumulate URL
```

Example of usage:

```bash
> get acc://3ed6b2003242d2166508e117a2a66f8ca742b72e8d90d736/ACME
{"url":"acc://3ed6b2003242d2166508e117a2a66f8ca742b72e8d90d736/ACME","wait":false}
{"data":{"balance":"1000000000","creditBalance":"0","keyBookUrl":"","nonce":0,"tokenUrl":"acc://ACME","txCount":1,"url":"acc://3ed6b2003242d2166508e117a2a66f8ca742b72e8d90d736/ACME"},"keyPage":null,"mdRoot":"0000000000000000000000000000000000000000000000000000000000000000","sponsor":"","type":"anonTokenAccount"}
```

### Tx

Send token from one anonymous token account to another one.

```bash
Usage:
  accumulate tx get [token account] [txid]      Get token tx by token account and txid
  accumulate tx create [from] [to] [amount]     Create new token tx
```

#### Tx Get&#x20;

Example of usage:

```shell
> tx get 46469416c03b2b386e6c10da8e873f0d61392fc1e8384b63123d8d1e8a7326dd
{"data":{"from":"acc://7117c50f04f1254d56b704dc05298912deeb25dbc1d26ef6/ACME","to":[{"amount":1000000000,"txid":"60d4c56055876cfa955721ff8613d9e372de02167951f360e4bcb27d2b1efb48","url":"acc://e3f53a4582a9193914effacbd2ef5ad8105a61cdf78ee414/ACME"}],"txid":"46469416c03b2b386e6c10da8e873f0d61392fc1e8384b63123d8d1e8a7326dd"},"keyPage":{"height":1,"index":0},"sig":"ce03ba0e52cdd4ce140de75f51727e2c40b1cc1f141e16916ad5f3a435935b81e99e43ce15274f973e1a06dab2dc174567f0544e1dfec39b516ef095fbf8670f","signer":{"nonce":1635714053572291600,"publicKey":"d03c683332ed36add8d0eeb9eee9e2669b5565decec03acc43d762f3f79f49c2"},"sponsor":"acc://7117c50f04f1254d56b704dc05298912deeb25dbc1d26ef6/ACME","status":{"code":"0"},"type":"tokenTx"}
```

#### Tx Create

Example of usage:

```bash
> tx create acc://3ed6b2003242d2166508e117a2a66f8ca742b72e8d90d736/ACME acc://e3f53a4582a9193914effacbd2ef5ad8105a61cdf78ee414/ACME 500000000>l
22fe5656270db192406d33ac9c93aee611c361ce9380a514ab8be417e0be52778e5d0e715434e4105a8f57dda15fcb3bd235a55f85226d0ec5c1c733f9ed78fb
{"data":{"codespace":"","hash":"D0A30534CDE714E2C56BBACA12C66B654849572381F17B04E02CA9E8FC210977","txid":"8bf87e52431bb3f6424025b8c9c680b4e8d541fb4c5f64c702271fa2207775f2"},"keyPage":null,"sponsor":"","type":"tokenTx"}
```

#### Tx History

Example of usage:

```bash
> tx history acc://3ed6b2003242d2166508e117a2a66f8ca742b72e8d90d736/ACME 0 1
{"data":[{"data":{"amount":"1000000000","from":"acc://7117c50f04f1254d56b704dc05298912deeb25dbc1d26ef6/ACME","to":"acc://3ed6b2003242d2166508e117a2a66f8ca742b72e8d90d736/ACME","tokenURL":"acc://ACME","txid":"1d6138b453b7bee86f70e3012c2f0b4264dd631f6551965fe39b8bd1da08bb49"},"keyPage":{"height":1,"index":0},"sig":"a48dbc485b083c96c7bede7938b6feaa19112950d2745378c7314b6d2ec51172ce358776ad1bc08f4b5e2c84c4eab0a7935fd1ac52d0e28ba0fe2c10c03a8e0b","signer":{"nonce":74,"publicKey":"21557951f8c6ca409e5156c4f8df60ed6fb7e6fea6eaaffe5c98c8577af4e525"},"sponsor":"acc://7117c50f04f1254d56b704dc05298912deeb25dbc1d26ef6/ACME","status":{"code":"0"},"type":"syntheticTokenDeposit"}],"limit":1,"start":0,"total":2,"type":"tokenAccountHistory"}
```

