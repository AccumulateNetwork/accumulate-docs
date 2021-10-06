# Command Line Wallet

Command Line Wallet allows to create, import, and export anonymous token accounts, create token txs and get data by Accumulate URL.

By default, Command Line Wallet connects to localhost Accumulate Node, but you can specify any remote server by using the flag.

### Basic commands and flags

```bash
Usage:
  accumulate [command] [flags]

Available Commands:
  account     Create and get token accounts
  faucet      Get tokens from faucet
  get         Get data by URL
  help        Help about any command
  tx          Create and get token txs
  
Flags:
  -d, --debug              Print accumulated API calls
  -h, --help               help for accumulate
  -s, --server string      Accumulated server (default "http://localhost:35554/v1")
  -t, --timeout duration   Timeout for all API requests (i.e. 10s, 1m) (default 5s)
```

### Account

Anonymous token accounts are stored into local database. CLI allows you to generate anon token accounts and export/import corresponsing private keys.

```bash
Usage:
  accumulate account get [url]                  Get anon token account by URL
  accumulate account generate                   Generate random anon token account
  accumulate account list                       Display all anon token accounts
  accumulate account import [private-key]       Import anon token account from private key hex
  accumulate account export [url]               Export private 
```

#### **Account generation**

```bash
> accumulate account generate
acme-9215794bc132db2dabc0ee62b5748cbb519e082957b195ec
```

#### Account export

```bash
> accumulate account export acme-9215794bc132db2dabc0ee62b5748cbb519e082957b195ec
7dad4f6267b28ea540d2709f115a37f3d61977bb8871eef716503e8eea80d291bd0f45b07503e29207c70c71317f3acdedeba7c6e6bf00ced2092440e2ceede2
```

#### Account import

```bash
> accumulate account import 7dad4f6267b28ea540d2709f115a37f3d61977bb8871eef716503e8eea80d291bd0f45b07503e29207c70c71317f3acdedeba7c6e6bf00ced2092440e2ceede2
acme-9215794bc132db2dabc0ee62b5748cbb519e082957b195ec
```

### Faucet

Faucet sends some testnet ACME tokens to requested token account.

```bash
Usage:
  accumulate faucet [url]               Get tokens from faucet to address
```

Example of usage:

```bash
> accumulate faucet acme-9215794bc132db2dabc0ee62b5748cbb519e082957b195ec
{"data":{"log":"","txid":"31f28aa4b51818bdfc3c0bc678796ddca584e82fcd27b8764eb6d25bd9141578"},"type":"faucet"}
```

### Get

Get data by Accumulate URL.

```bash
Usage:
  accumulate get [url]          Get data by Accumulate URL
```

Example of usage:

```bash
> accumulate get acme-9215794bc132db2dabc0ee62b5748cbb519e082957b195ec
{"data":{"balance":"1000000000","tokenURL":"dc/ACME","url":"acme-9215794bc132db2dabc0ee62b5748cbb519e082957b195ec/dc/ACME"},"type":"tokenAccount"}
```

### Tx

Send token from one anonymous token account to another one.

```bash
Usage:
  accumulate tx get [token account] [txid]                    Get token tx by token account and txid
  accumulate tx create [from] [to] [amount]     Create new token tx
```

Example of usage:

```bash
> accumulate tx create acme-9215794bc132db2dabc0ee62b5748cbb519e082957b195ec acme-c011b464035ee492553132350907bbdb2220be2322ececc5 10000
{"data":{"log":"","txid":"4daac8520653bf2b202b3fc8c17c882423b15cfb145917922b2d0b5731bbba0c"},"type":"tokenTx"}
```

