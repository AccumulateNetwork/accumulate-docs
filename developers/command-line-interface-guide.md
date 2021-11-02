# Command Line Interface (CLI) Guide

The Command-Line Interface Tool allows for the following: token, identity, and key management. By default, the Command-Line Interface connects to a localhost Accumulate Node, but you can specify any remote server by using the flag.

## How to build the CLI tool

```bash
$ git clone https://github.com/AccumulateNetwork/accumulated.git
$ cd accumulated/cmd/cli
$ go build
```

## Start CLI tool

```bash
$ ./cli.exe
```
```bash
CLI for Accumulate Network

Usage:
  accumulate [command] [flags]

Available Commands:
  account     Create and get token accounts
  adi         Create and manage ADI
  completion  generate the autocompletion script for the specified shell
  credits     Send credits to a recipient
  faucet      Get tokens from faucet
  get         Get data by URL
  help        Help about any command
  key         Create and manage Keys, Books, and Pages
  tx          Create and get token txs
  version     get version of the accumulate node

Flags:
  -d, --debug              Print accumulated API calls
  -h, --help               help for accumulate
  -s, --server string      Accumulated server (default "http://localhost:35554/v1")
  -t, --timeout duration   Timeout for all API requests (i.e. 10s, 1m) (default 5s)

Use "accumulate [command] --help" for more information about a command.
```

## Basic Operations 

### Account

Anonymous token accounts are stored in a local database. CLI allows you to generate anon token accounts and export/import corresponding private keys, create transactions, see a list of all of your accounts, and pull information about a URL.

```bash
$ ./cli.exe account
```

```bash
  accumulate account get [url]                  Get anon token account by URL
  accumulate account generate                   Generate random anon token account
  accumulate account list                       Display all anon token accounts
  accumulate account create [{actor adi}] [wallet key label] [key index (optional)] [key height (optional)] [token account url] [tokenUrl] [keyBook (optional)]  Create a token account for an ADI
  accumulate account import [private-key]       Import anon token account from private key hex
  accumulate account export [url]               Export private key hex of anon token account
```

#### Create Account

```bash
Usage:
accumulate account generate                   Generate random anon token account
```

Example of usage:

```bash
$ ./cli.exe account generate
acc://c078e544351861f38ed40521beee54f9fb0276103d4189d9/ACME
```

#### Account list

```bash
Usage:
accumulate account list                       Display all anon token accounts
```

Example of usage:

```bash
$ ./cli.exe account list 
acc://68fe2628a354d44ab349b08566ac35139a22b9896b1eff0d/ACME
acc://c078e544351861f38ed40521beee54f9fb0276103d4189d9/ACME
```

#### Fund tokens from Faucet

Faucet sends some TestNet ACME tokens to the requested anonymous token account.

```bash
Usage:
faucet [url]               Get tokens from faucet to address
```

Example of usage:

```bash
$ ./cli.exe faucet acc://c078e544351861f38ed40521beee54f9fb0276103d4189d9/ACME -s http://18.119.26.7:33004/v1
{"data":{"codespace":"","hash":"64D2F5A1245D0C877F2A967D14E6B9121687A122D9032D2D4A98AF7A719EF2FA","txid":"f6bb8797f85b3bdb08e344e42ce3ca7cb42d4704128c7cd7bc1c1ada9d5a3e6f"},"keyPage":null,"sponsor":"","type":""}
```

#### Get Account info

```bash
Usage:
accumulate account get [url]                  Get anon token account by URL
```

Example of usage:

```bash
$ ./cli.exe account get acc://c078e544351861f38ed40521beee54f9fb0276103d4189d9/ACME -s http://18.119.26.7:33004/v1
{"data":{"balance":"1000000000","creditBalance":"0","keyBookUrl":"","nonce":0,"tokenUrl":"acc://ACME","txCount":1,"url":"acc://c078e544351861f38ed40521beee54f9fb0276103d4189d9/ACME"},"keyPage":null,"mdRoot":"0000000000000000000000000000000000000000000000000000000000000000","sponsor":"","type":"anonTokenAccount"}
```

#### Get Transaction info

```
Usage:
accumulate tx get [txid]                      Get token transaction by txid
```

Example of usage:

```bash
$ ./cli.exe tx get f6bb8797f85b3bdb08e344e42ce3ca7cb42d4704128c7cd7bc1c1ada9d5a3e6f -s http://18.119.26.7:33004/v1
{"data":{"from":"acc://7117c50f04f1254d56b704dc05298912deeb25dbc1d26ef6/ACME","to":[{"amount":1000000000,"txid":"d1d2b8c3f419e7caea4573be197da4d49142d5ae290974b2d8c131239d3fadfe","url":"acc://c078e544351861f38ed40521beee54f9fb0276103d4189d9/ACME"}],"txid":"f6bb8797f85b3bdb08e344e42ce3ca7cb42d4704128c7cd7bc1c1ada9d5a3e6f"},"keyPage":{"height":1,"index":0},"sig":"4ddd5d7916e02227c07398595e83bc115c20d1a463e5f7085bbf245efbf94dda8f997b7ecb6754b4f37bece1431c44bb5275bb53dbed45dc39db539adfd78f07","signer":{"nonce":1635849154607908400,"publicKey":"d03c683332ed36add8d0eeb9eee9e2669b5565decec03acc43d762f3f79f49c2"},"sponsor":"acc://7117c50f04f1254d56b704dc05298912deeb25dbc1d26ef6/ACME","status":{"code":"0"},"type":"tokenTx"}
```

#### Create a new account and transfer some tokens

```
Usage:
accumulate tx create [from] [to] [amount]     Create new token tx
```

Example of usage:

```bash
$ ./cli.exe account generate
acc://df8d19e2cb0435d178d1c6c7a114872d083a27a65a854707/ACME
```

```bash
$ ./cli.exe tx create acc://c078e544351861f38ed40521beee54f9fb0276103d4189d9/ACME acc://df8d19e2cb0435d178d1c6c7a114872d083a27a65a854707/ACME 2000 -s http://18.119.26.7:33004/v1
{"data":{"codespace":"","hash":"9545262EC02FA1C7E21E797DC0C7A3D42EF1BAA365BB32CF52996407D5B56DB4","txid":"7bb88c24774c234b4363748b895742027e02bb897359ae0451f76c74ed85d985"},"keyPage":null,"sponsor":"","type":"tokenTx"}
```

#### Verify the account balalnce

```bash
Usage:
accumulate account get [url]                  Get anon token account by URL
```

Example of usage:

```bash
$ ./cli.exe get acc://c078e544351861f38ed40521beee54f9fb0276103d4189d9/ACME -s http://18.119.26.7:33004/v1
{"url":"acc://c078e544351861f38ed40521beee54f9fb0276103d4189d9/ACME","wait":false}
{"data":{"balance":"999998000","creditBalance":"0","keyBookUrl":"","nonce":0,"tokenUrl":"acc://ACME","txCount":2,"url":"acc://c078e544351861f38ed40521beee54f9fb0276103d4189d9/ACME"},"keyPage":null,"mdRoot":"0000000000000000000000000000000000000000000000000000000000000000","sponsor":"","type":"anonTokenAccount"}

$ ./cli.exe get acc://df8d19e2cb0435d178d1c6c7a114872d083a27a65a854707/ACME -s http://18.119.26.7:33004/v1
{"url":"acc://df8d19e2cb0435d178d1c6c7a114872d083a27a65a854707/ACME","wait":false}
{"data":{"balance":"2000","creditBalance":"0","keyBookUrl":"","nonce":0,"tokenUrl":"acc://ACME","txCount":1,"url":"acc://df8d19e2cb0435d178d1c6c7a114872d083a27a65a854707/ACME"},"keyPage":null,"mdRoot":"0000000000000000000000000000000000000000000000000000000000000000","sponsor":"","type":"anonTokenAccount"}
```

