# CLI Reference

The Command-Line Interface Tool allows you to interact with the Accumulate protocol and includes operations around token, identity, and key management. By default, the Command-Line Interface connects to the dedicated testnet server, but you can manually connect to a different server with `-s`

{% hint style="info" %}
If you'd like to connect to a specific testnet server, you can find a list of the available servers in the [Networks.go file](https://github.com/AccumulateNetwork/accumulated/blob/develop/networks/networks.go). Or you can use the public testnet server: `https://testnet.accumulatenetwork.io/v1`.
{% endhint %}

### Basic commands and flags

```bash
> help
```

```bash
CLI for Accumulate Network

Usage:
  accumulate [command] [flags]

Available Commands
  account     Create and get token accounts
  adi         Create and manage ADI
  book        Manage key books for a ADI chains
  completion  generate the autocompletion script for the specified shell
  faucet      Get tokens from faucet
  help        Help about any command
  key         Create and manage Keys for ADI Key Books, and Pages
  page        Create and manage Keys, Books, and Pages
  tx          Create and get token txs
  version     get version of the accumulate node

Flags:
  -d, --debug              Print accumulated API calls
  -h, --help               help for accumulate
  -s, --server string      Accumulated server (default "http://localhost:35554/v1")
  -t, --timeout duration   Timeout for all API requests (i.e. 10s, 1m) (default 5s)

  Use "accumulate [command] --help" for more information about a command.
```

### Account

Anonymous token accounts are stored in a local database. CLI allows you to generate anon token accounts and export/import corresponding private keys, create transactions, see a list of all of your accounts, and pull information about a URL.

```bash
> account
```

```bash
  accumulate account get [url]                  Get anon token account by URL
  accumulate account generate                   Generate random anon token account
  accumulate account list                       Display all anon token accounts
  accumulate account create [{actor adi}] [wallet key label] [key index (optional)] [key height (optional)] [token account url] [tokenUrl] [keyBook (optional)]  Create a token account for an ADI
```

**Account get**

```bash
Usage:
accumulate account get [url]                  Get anon token account by URL
```

Example of usage:

```bash
> get acc://68fe2628a354d44ab349b08566ac35139a22b9896b1eff0d/ACME
```

```json
//Response:
{
  "data": {
    "balance": "1000000000",
    "creditBalance": "0",
    "keyBookUrl": "",
    "nonce": 0,
    "tokenUrl": "acc://ACME",
    "txCount": 1,
    "url": "acc://68fe2628a354d44ab349b08566ac35139a22b9896b1eff0d/ACME"
  },
  "keyPage": null,
  "mdRoot": "0000000000000000000000000000000000000000000000000000000000000000",
  "sponsor": "",
  "type": "anonTokenAccount"
}
```

Example of usage:

```bash
> get acc://ADITEST/TOKENS/ACME
{"url":"ADITEST/TOKENS","wait":false}
{"data":{"balance":"1000000000","keyBookUrl":"","tokenUrl":"acc://ACME","txCount":1,"url":"acc://ADITEST/TOKENS"},"keyPage":null,"mdRoot":"0000000000000000000000000000000000000000000000000000000000000000","sponsor":"","type":"tokenAccount"}
```

**Account generate**

```bash
Usage:
accumulate account generate                   Generate random anon token account
```

Example of usage:

```bash
> account generate
acc://68fe2628a354d44ab349b08566ac35139a22b9896b1eff0d/ACME
```

#### Account list

```bash
Usage:
accumulate account list                       Display all anon token accounts
```

Example of usage:

```bash
> account list
acc://68fe2628a354d44ab349b08566ac35139a22b9896b1eff0d/ACME
acc://78ef49e7ff69a7099774b72ec31edffb6c5a66a964aaa6e9/ACME
```

#### Account Create (ADI Token Account)

```
Usage:
accumulate account create [{actor adi}] [wallet key label] [key index (optional)] [key height (optional)] [token account url] [tokenUrl] [keyBook (optional)]  Create a token account for an ADI
```

Example of usage:

```bash
> account create ADITEST key1234 0 1 ADITEST/TOKENS acc://ACME ADITEST/ADIKEYBOOK1
{"url":"acc://ACME","wait":false}
{"data":{"precision":8,"propertiesUrl":"","symbol":"ACME","url":"acc://ACME"},"keyPage":null,"mdRoot":"0000000000000000000000000000000000000000000000000000000000000000","sponsor":"","type":"token"}
{"data":{"codespace":"","hash":"D4671ABD87E02BF6ACC3864BA84FF7F17D9A2224055973DB9079079D93F3D75B","txid":"5668f7a936c45e513d654a98ee758d8a3612833c5256ef65aed32c639e721aaa"},"keyPage":null,"sponsor":"","type":"tokenAccount"}
```

### ADI

Create an Accumulate Digital Identifier. The Accumulate network is managed by an enhanced version of Distributed Digital Identities and Identifiers (DDIIs) that we refer to as Accumulate Digital Identifiers (ADIs).

```bash
> adi
```

```
  accumulate adi get [URL]                      Get existing ADI by URL
  accumulate adi create [actor-lite-account] [adi url to create] [public-key or wallet key label] [key-book-name (optional)] [key-page-name (optional)]  Create new ADI from lite account
  accumulate adi create [actor-adi-url] [wallet signing key label] [key index (optional)] [key height (optional)] [adi url to create] [public key or wallet key label] [key book url (optional)] [key page url (optional)] Create new ADI for another ADI
  accumulate adi import [adi-url] [private-key] Import Existing ADI
```

#### ADI get

```
Usage:
accumulate adi get [URL]                      Get existing ADI by URL
```

Example of usage:

```bash
> adi get
{"data":{"keyBookName":"","keyPageName":"","publicKey":"ec52b1f5b263010912431bf8e4af6ed84b3b3d64baff41b306fec359a512e7b5","url":"acc://ADITEST"},"keyPage":null,"mdRoot":"0000000000000000000000000000000000000000000000000000000000000000","sponsor":"","type":"adi"}
```

#### ADI create (Create New ADI from Lite Account)

```
Usage:
accumulate adi create [actor-lite-account] [adi url to create] [public-key or wallet key label] [key-book-name (optional)] [key-page-name (optional)]  Create new ADI from lite account
```

Example of usage:

```bash
> adi create acc://68fe2628a354d44ab349b08566ac35139a22b9896b1eff0d/ACME ADITEST key1234 ADIKEYBOOK1 ADIKEYPAGE1
{"data":{"codespace":"","hash":"A656742EACDDB73933D9AF7598DC29AEDFA7060E458DF829A58E70B03BCC878D","txid":"c6d726ac34d1b203b3c4d18233abbfdfa34d8f0eb3f3dcfe2f7aafc1fe16c178"},"keyPage":null,"sponsor":"","type":"tokenTx"}
```

#### ADI create (Create new ADI for another ADI)

```
Usage:
accumulate adi create [actor-adi-url] [wallet signing key label] [key index (optional)] [key height (optional)] [adi url to create] [public key or wallet key label] [key book url (optional)] [key page url (optional)] Create new ADI for another ADI
```

Example of usage:

```bash
> adi create ADITEST key1234 0 1 ADITEST2 key5678 ADIKEYBOOK2 ADIKEYPAGE2
{"data":{"codespace":"","hash":"D196F92987F6EB5E73838D8B62AB782007E0363003BC9B40F52AC3DAEA18A66F","txid":"004f0df62645f5a128370528123eab320e79ecad5b74110f12d6f74de1860078"},"keyPage":null,"sponsor":"","type":"tokenTx"}
```

### Book

```bash
> book
```

```
Usage:
accumulate book get [URL]                     Get existing Key Book by URL
accumulate book create [actor adi url] [signing key label] [key index (optional)] [key height (optional)] [new key book url] [key page url 1] ... [key page url n + 1] Create new key book and assign key pages 1 to N+1 to the book
```

**Get Key Book**

```
Usage:
accumulate key get book [URL]                 Get existing Key Book by URL
```

Example of usage:

```bash
> get ADITEST/ADIKEYBOOK1
{"url":"ADITEST/ADIKEYBOOK1","wait":false}
{"data":{"sigSpecId":[0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0],"sigSpecs":["df9531256df68eed2aa496b84bfbd7b6f989bdd08088d62dbbfc85451b820ac8"],"type":11,"url":"acc://ADITEST/ADIKEYBOOK1"},"keyPage":null,"mdRoot":"0000000000000000000000000000000000000000000000000000000000000000","sponsor":"","type":"sigSpecGroup"}
```

**Key Book Create**

```
Usage:
accumulate key book create [actor adi url] [signing key label] [key index (optional)] [key height (optional)] [new key book url] [key page url 1] ... [key page url n] Create new key page with 1 to N public keys
```

Example of usage:

```bash
> key book create ADITEST key1234 1 1 ADITEST/KEYBOOK1.1 ADITEST/KEYPAGE1.1 ADITEST/KEYPAGE1.2 ADITEST/KEYPAGE1.3
{"data":{"code":"2","codespace":"","hash":"CD8322D22945E81142AAF38459FD99572AF20FABF8832827D6C0A1933EC8F813","log":"acc://ADITEST check of createSigSpecGroup transaction failed: invalid sig spec index","mempool":"","txid":"4fb9e1ee7bec80a664ac73ffcdde84754ce0c003dd3a710a0cb9b541f806ba73"},"keyPage":null,"sponsor":"","type":"sigSpecGroup"}
```

### Completion

```bash
> completion
```

```
Available Commands:
  bash        generate the autocompletion script for bash
  fish        generate the autocompletion script for fish
  powershell  generate the autocompletion script for powershell
  zsh         generate the autocompletion script for zsh

Flags:
  -h, --help   help for completion

Global Flags:
  -d, --debug              Print accumulated API calls
  -s, --server string      Accumulated server (default "http://localhost:35554/v1")
  -t, --timeout duration   Timeout for all API requests (i.e. 10s, 1m) (default 5s)

Use "accumulate completion [command] --help" for more information about a command.
```

### Directory

Accumulate directory for Accumulate Digital Identifiers

```bash
> directory
```

```
Usage:
accumulate adi directory [url]              Get directory of sub-chains associate with a URL
```

Example of usage:

```bash
> adi directory ADITEST
{"data":{"entries":["acc://ADITEST/ADIKEYBOOK1","acc://ADITEST/ADIKEYPAGE1", “acc://ADITEST/TOKENS"]},"keyPage":null,"sponsor":"","type":"directory"}
```

### Faucet

Faucet sends some TestNet ACME tokens to the requested anonymous token account.

```bash
> faucet
```

```bash
Usage:
faucet [url]               Get tokens from faucet to address
```

Example of usage:

```bash
> accumulate faucet acc://3ed6b2003242d2166508e117a2a66f8ca742b72e8d90d736/ACME
{"data":{"codespace":"","hash":"C89966F8435FE6BC195DEB817CBCCBC3D9FF210EDA2B2B60F4CEC5E4E714F9A4","txid":"1d6138b453b7bee86f70e3012c2f0b4264dd631f6551965fe39b8bd1da08bb49"},"keyPage":null,"sponsor":"","type":""}
```

### Help

CLI Help

```bash
> help
```

```
CLI for Accumulate Network

Usage:
  accumulate [command] [flags]

Available Commands
  account     Create and get token accounts
  adi         Create and manage ADI
  book        Manage key books for a ADI chains
  completion  generate the autocompletion script for the specified shell
  faucet      Get tokens from faucet
  help        Help about any command
  key         Create and manage Keys for ADI Key Books, and Pages
  page        Create and manage Keys, Books, and Pages
  tx          Create and get token txs
  version     get version of the accumulate node

Flags:
  -d, --debug              Print accumulated API calls
  -h, --help               help for accumulate
  -s, --server string      Accumulated server (default "http://localhost:35554/v1")
  -t, --timeout duration   Timeout for all API requests (i.e. 10s, 1m) (default 5s)

  Use "accumulate [command] --help" for more information about a command.
```

### Key

Managed the Keys, Key Pages, and Key Book for your Accumulate Digital

```bash
> key
```

```
  Usage:
  accumulate key generate [key name]     Generate a new key and give it a name in the wallet
  accumulate key list                   List generated keys associated with the wallet
  accumulate key import mnemonic [mnemonic phrase...]     Import the mneumonic phrase used to generate keys in the wallet
  accumulate key import private [private key hex] [key name]      Import a key and give it a name in the wallet
  accumulate key export all                                 export all keys in wallet
  accumulate key export private [key name]                      export the private key by key name
  accumulate key export mnemonic                            export the mnemonic phrase if one was entered
  accumulate key export seed                       export the seed generated from the mnemonic phrase
```

**Key Generation**

```
Usage:
accumulate key generate [label]     Generate a new key and give it a label in the wallet
```

Example of usage:

```bash
> key generate key1234
ec52b1f5b263010912431bf8e4af6ed84b3b3d64baff41b306fec359a512e7b5
```

**Key List**

```
Usage:
accumulate key list                   List generated keys associated with the wallet
```

Example of usage:

```bash
> key list
key1234                  ec52b1f5b263010912431bf8e4af6ed84b3b3d64baff41b306fec359a512e7b5
```

**Key Import Mnemonic **

```
Usage:
accumulate key import mnemonic [mnemonic phrase...]     Import the mnemonic phrase used to generate keys in the wallet
```

Example of Usage:

```bash
> key mnemonic humor demand lesson identify rookie road truth beef benefit thank camera tumble
Mnemonic imported
```

**Key Import Private Key**

```
Usage:
accumulate key import private [private key hex] [key name]      Import a key and give it a name in the wallet
```

Example of Usage:

```
// Some code
```

**Key Export All **

```
Usage:
accumulate key export all                                 export all keys in wallet
```

Example of usage:

```bash
> key export all
{"name":"MarianP","privateKey":"e3e6c72c16d848bd54fa50ec4aa43ae5832ad70da3cd14705dac567de9192e86","publicKey":"0c5ebf71e4068306a5916309717af8c25ad17cb376fe9e96957168588a4048f1"}
{"name":"acc://5eed661e873c4437fb31f034cc31e049b49c2260d035b2c6/ACME","privateKey":"abcd9388fcb6c718ef49a7cfa50fa9832a123de63769eabdc025bfb848e2b0a8","publicKey":"1f339c9684aa756d57ae0a37961bfc9aad84b575f22fa378701f3944af095106"}
```

**Key Export Private **

```
Usage:
accumulate key export private [key name]                      export the private key by key name
```

Example of usage:

```bash
> key export private 1234
{"name":"key1234","privateKey":"25c8d1b59cf3585b1adcce63ad06b6e67c8ed07d98e128a6324b51c993fdf154","publicKey":"ec52b1f5b263010912431bf8e4af6ed84b3b3d64baff41b306fec359a512e7b5"}
```

**Key Export Mnemonic **

```
Usage:
accumulate key export mnemonic                            export the mnemonic phrase if one was entered
```

Example of usage:

```bash
> key export mnemonic
mnemonic phrase: humor demand lesson identify rookie road truth beef benefit thank camera tumble
```

**Key Export Seed **

```
accumulate key export seed                       export the seed generated from the mnemonic phrase
```

Example of usage:

```bash
> key export seed
seed: b1310fcca7d5938d552561757d1e62a11a6fd3939cabdcfbbad94d1a6fb6a873f81b15f286ab4bed8e6139e4a6348387d555b72cf0e98793f5828264cfa78c77
```

### Page

```
> Page
```

```
accumulate page create [actor adi url] [signing key label] [key index (optional)] [key height (optional)] [new key page url] [public key 1] ... [public key hex or label n + 1] Create new key page with 1 to N+1 public keys 
                 example usage: accumulate key page create acc://RedWagon redKey5 acc://RedWagon/RedPage1 redKey1 redKey2 redKey3
  accumulate page get [URL]                     Get existing Key Page by URL
  accumulate page key update [key page url] [signing key label] [key index (optional)] [key height (optional)] [old key label] [new public key or label] Update key in a key page with a new public key
                 example usage: accumulate key update page  acc://RedWagon redKey5 acc://RedWagon/RedPage1 redKey1 redKey2 redKey3
  accumulate page key add [key page url] [signing key label] [key index (optional)] [key height (optional)] [new key label] Add key to a key page
                 example usage: accumulate key add page acc://RedWagon redKey5 acc://RedWagon/RedPage1 redKey1 redKey2 redKey3
  accumulate page key remove [key page url] [signing key label] [key index (optional)] [key height (optional)] [old key label] Remove key from a key page
                 example usage: accumulate key add page acc://RedWagon redKey5 acc://RedWagon/RedPage1 redKey1 r
```

**Get Key Page**

```
Usage:
accumulate key get page [URL]                 Get existing Key Page by URL
```

Example of usage:

```bash
> get ADITEST/ADIKEYPAGE1
{"url":"ADITEST/ADIKEYPAGE1","wait":false}
{"data":{"creditBalance":0,"keys":[{"nonce":0,"publicKey":"ec52b1f5b263010912431bf8e4af6ed84b3b3d64baff41b306fec359a512e7b5"}],"sigSpecId":"d58e359c82d3efdbb38e355cfb5f50b42ee5fefda90582b4ef571b9f5478552e","type":10,"url":"acc://ADITEST/ADIKEYPAGE1"},"keyPage":null,"mdRoot":"0000000000000000000000000000000000000000000000000000000000000000","sponsor":"","type":"sigSpec"}
```

**Key Page Create**

```
Usage:
accumulate key page create [actor adi url] [signing key label] [key index (optional)] [key height (optional)] [new key page url] [public key label 1] ... [public key label n] Create new key page with 1 to N public keys within the wallet
```

Example of usage:

```bash
> key page create ADITEST key1234 ADITEST/ADIKEYPAGE1.4 KEY1.4 KEY1.41 KEY1.42
{"data":{"codespace":"","hash":"1893687A65DAEBA8730C914750A38724FADEAD81B49913EC614BC4F150C420C3","txid":"a71101eb4636d46aa4b31db4cd28364091530b4ce1cfa1b22a0955a0bdbb2186"},"keyPage":null,"sponsor":"","type":"sigSpec"}
```

**Page Key Update**

```
accumulate key page update [key page url] [signing key label] [key index (optional)] [key height (optional)] [old key label] [new public key or label] Update key page with a new public key
```

Example of usage:

```bash
> page key update ADITEST/ADIKEYPAGE1 key5678 1 1 key5678 key1234
{"data":{"code":"2","codespace":"","hash":"15C1D6A9014CB99C3F7FBD804E87EA644126537B4D5F342BC93A5D0DEDBE0B5B","log":"acc://ADITEST/ADIKEYPAGE1 check of updateKeyPage transaction failed: invalid sig spec index","mempool":"","txid":"4d23f95a0201e4589d26c6b28f68c6fc658d05f74997c1ebd8c3711b574e963a"},"keyPage":null,"sponsor":"","txid":null,"type":"sigSpec"
```

**Page Key Add**

```
accumulate key page add [key page url] [signing key label] [key index (optional)] [key height (optional)] [new key label] Add key to key page
```

Example of usage:

```bash
> page key add ADITEST/ADIKEYPAGE1 key1234 1 1 key5678
{"data":{"code":"2","codespace":"","hash":"FF52531081161330E1B52F1A4E9108D6782495495A909176F7E9650DE01BE8C0","log":"acc://ADITEST/ADIKEYPAGE1 check of updateKeyPage transaction failed: invalid sig spec index","mempool":"","txid":"83d357c824a444014eafe1b8a8a1ea972d831d91f1258a1b2d46618a7450c16b"},"keyPage":null,"sponsor":"","txid":null,"type":"sigSpec"
```

**Page Key Remove**

```
accumulate key page remove [key page url] [signing key label] [key index (optional)] [key height (optional)] [old key label] Remove key in key page
```

Example of usage:

```bash
> page key remove ADITEST/ADIKEYPAGE1 key1234 1 1 key1234
{"data":{"code":"2","codespace":"","hash":"5FDCB8ACBF729C3F162DB5BE22EACD43796E43761BA6E9CD09DCC3F5EE468D05","log":"acc://ADITEST/ADIKEYPAGE1 check of updateKeyPage transaction failed: invalid sig spec index","mempool":"","txid":"99084b8865ec9503dd7f1c752f2243036523bff3548af134a8fa0b5fa3535c70"},"keyPage":null,"sponsor":"","txid":null,"type":"sigSpec"}
```

### Tx

Send token from one anonymous token account to another one.

```bash
> tx
```

```bash
Usage:
accumulate tx get [txid]                      Get token transaction by txid
accumulate tx create [from] [to] [amount]     Create new token tx
accumulate tx history [url] [starting transaction number] [ending transaction number] Get transaction history
```

#### Tx Get

```
Usage:
accumulate tx get [txid]                      Get token transaction by txid
```

Example of usage:

```shell
> tx get 46469416c03b2b386e6c10da8e873f0d61392fc1e8384b63123d8d1e8a7326dd
{"data":{"from":"acc://7117c50f04f1254d56b704dc05298912deeb25dbc1d26ef6/ACME","to":[{"amount":1000000000,"txid":"60d4c56055876cfa955721ff8613d9e372de02167951f360e4bcb27d2b1efb48","url":"acc://e3f53a4582a9193914effacbd2ef5ad8105a61cdf78ee414/ACME"}],"txid":"46469416c03b2b386e6c10da8e873f0d61392fc1e8384b63123d8d1e8a7326dd"},"keyPage":{"height":1,"index":0},"sig":"ce03ba0e52cdd4ce140de75f51727e2c40b1cc1f141e16916ad5f3a435935b81e99e43ce15274f973e1a06dab2dc174567f0544e1dfec39b516ef095fbf8670f","signer":{"nonce":1635714053572291600,"publicKey":"d03c683332ed36add8d0eeb9eee9e2669b5565decec03acc43d762f3f79f49c2"},"sponsor":"acc://7117c50f04f1254d56b704dc05298912deeb25dbc1d26ef6/ACME","status":{"code":"0"},"type":"tokenTx"}
```

#### Tx Create

```
Usage:
accumulate tx create [from] [to] [amount]     Create new token tx
```

Example of usage:

```bash
> tx create acc://68fe2628a354d44ab349b08566ac35139a22b9896b1eff0d/ACME acc://78ef49e7ff69a7099774b72ec31edffb6c5a66a964aaa6e9/ACME 500000000
5917639ec8c66576b8e44797cfc198f0b85b0cbe4ab29ac8a1e8413a7b779f888d378ef83bcd38edf6023ed77a4e422059770da9d198ead8fd76245a353ced61
{"data":{"codespace":"","hash":"AD97A5F97FFCBCD713690216897DAA2FB4E6194F9C6F5E4279F57DD6895082DF","txid":"1968a55178de4ed410c859d8bd34a0bec311cd01fd706b165e9242c315273232"},"keyPage":null,"sponsor":"","type":"tokenTx"}
```

#### Tx History

```
Usage:
accumulate tx history [url] [starting transaction number] [ending transaction number] Get transaction history
```

Example of usage:

```bash
> tx history acc://68fe2628a354d44ab349b08566ac35139a22b9896b1eff0d/ACME 0 1
{"data":[{"data":{"amount":"1000000000","from":"acc://7117c50f04f1254d56b704dc05298912deeb25dbc1d26ef6/ACME","to":"acc://68fe2628a354d44ab349b08566ac35139a22b9896b1eff0d/ACME","tokenURL":"acc://ACME","txid":"8aef025e2d4e90d75f703c51aae321e44eb26c2f79de0034ac7bb7aae4c00d94"},"keyPage":{"height":1,"index":0},"sig":"ef8d401dc1022131b5cc3083c3453cfb707fa68d06be47c584e9c38e8e04622f20afbddaba5e664595887483848dc109ca5492e0182686d2ac59c95710a23805","signer":{"nonce":72,"publicKey":"7408e7dc62924a98b6c24fa814eec2d40363f9769875613d4d5ee04fdc1db94a"},"sponsor":"acc://7117c50f04f1254d56b704dc05298912deeb25dbc1d26ef6/ACME","status":{"code":"0"},"type":"syntheticTokenDeposit"}],"limit":1,"start":0,"total":2,"type":"tokenAccountHistory"}
```
