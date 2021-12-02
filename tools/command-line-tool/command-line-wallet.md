# CLI Reference

The Command-Line Interface Tool allows you to interact with the Accumulate network and includes operations around token, identity, and key management. By default, the Command-Line Interface connects to the dedicated testnet server, but you can manually connect to a different server with `-s`

{% hint style="info" %}
If you'd like to connect to a specific testnet server, you can find a list of the available servers in the [Networks.go file](https://github.com/AccumulateNetwork/accumulated/blob/develop/networks/networks.go). Or you can use the public testnet server: `https://testnet.accumulatenetwork.io/v1`.
{% endhint %}

### Basic commands and flags

```bash
$ ./cli.exe help
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
  credits     Send credits to a recipient
  faucet      Get tokens from faucet
  get         Get data by URL
  help        Help about any command
  key         Create and manage Keys for ADI Key Books, and Pages
  page        Create and manage Keys, Books, and Pages
  tx          Create and get token txs
  version     get version of the accumulate node

Flags:
  -d, --debug              Print accumulated API calls
  -h, --help               help for accumulate
  -s, --server string      Accumulated server (default "https://testnet.accumulatenetwork.io/v1")
  -t, --timeout duration   Timeout for all API requests (i.e. 10s, 1m) (default 5s)

  Use "accumulate [command] --help" for more information about a command.
```

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
```

**Account get**

```bash
Usage:
accumulate account get [url]                  Get anon token account by URL
```

Example of usage:

```bash
$ ./cli.exe account get acc://5a48d2999da25641db06a8e4baf54a275bfc6ed90cbcd21a/ACMEE
```

```bash
        Account Url     :       acc://5a48d2999da25641db06a8e4baf54a275bfc6ed90cbcd21a/ACME
        Token Url       :       acc://ACME
        Balance         :       19.9 ACME
        Credits         :       0
        Nonce           :       0
```

Example of usage:

```bash
$ ./cli.exe get acc://ADITEST/TOKENS/ACME
{
   "url":"ADITEST/TOKENS",
   "wait":false
}{
   "data":{
      "balance":"1000000000",
      "keyBookUrl":"",
      "tokenUrl":"acc://ACME",
      "txCount":1,
      "url":"acc://ADITEST/TOKENS"
   },
   "keyPage":null,
   "mdRoot":"0000000000000000000000000000000000000000000000000000000000000000",
   "sponsor":"",
   "type":"tokenAccount"
}
```

**Account generate**

```bash
Usage:
accumulate account generate                   Generate random anon token account
```

Example of usage:

```bash
$ ./cli.exe account generate
acc://26ddb87b5d12236f752680c97443a0212a93df4bdd7d784a/ACME :   3adc1fcd47c711e662b94335b1f270bd07bf27c279f65d5f754e091cc1e95b35
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
acc://78ef49e7ff69a7099774b72ec31edffb6c5a66a964aaa6e9/ACME
```

#### Account Create (ADI Token Account)

```
Usage:
accumulate account create [{actor adi}] [wallet key label] [key index (optional)] [key height (optional)] [token account url] [tokenUrl] [keyBook (optional)]  Create a token account for an ADI
```

Example of usage:

```bash
$ ./cli.exe account create ADITEST key1234 0 1 ADITEST/TOKENS acc://ACME ADITEST/ADIKEYBOOK1
{"url":"acc://ACME","wait":false}
{"data":{"precision":8,"propertiesUrl":"","symbol":"ACME","url":"acc://ACME"},"keyPage":null,"mdRoot":"0000000000000000000000000000000000000000000000000000000000000000","sponsor":"","type":"token"}
{"data":{"codespace":"","hash":"D4671ABD87E02BF6ACC3864BA84FF7F17D9A2224055973DB9079079D93F3D75B","txid":"5668f7a936c45e513d654a98ee758d8a3612833c5256ef65aed32c639e721aaa"},"keyPage":null,"sponsor":"","type":"tokenAccount"}
```

### ADI

Create an Accumulate Digital Identifier. The Accumulate network is managed by an enhanced version of Distributed Digital Identities and Identifiers (DDIIs) that we refer to as Accumulate Digital Identifiers (ADIs).

```bash
$ ./cli.exe adi
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
        ADI Url         :       acc://ADITEST
        Key Book Url    :       acc://ADITEST/keybook1
```

#### ADI create (Create New ADI from Lite Account)

```
Usage:
accumulate adi create [actor-lite-account] [adi url to create] [public-key or wallet key label] [key-book-name (optional)] [key-page-name (optional)]  Create new ADI from lite account
```

Example of usage:

```bash
$ ./cli.exe adi create acc://68fe2628a354d44ab349b08566ac35139a22b9896b1eff0d/ACME ADITEST key1234 ADIKEYBOOK1 ADIKEYPAGE1
2021/11/18 14:42:59
        Transaction Identifier  :       48217eb91f3a75fe22beddfba5166a34661d2dfd9b7ae222e8dccbe5be7ce310
        Tendermint Reference    :       df2d36bfbfeaa5b42307bad269d163c18dbd710c2c961194728e16b93664a387
        Error code              :       ok
```

#### ADI create (Create new ADI for another ADI)

```
Usage:
accumulate adi create [actor-adi-url] [wallet signing key label] [key index (optional)] [key height (optional)] [adi url to create] [public key or wallet key label] [key book url (optional)] [key page url (optional)] Create new ADI for another ADI
```

Example of usage:

```bash
$ ./cli.exe adi create ADITEST key1234 0 1 ADITEST2 key5678 ADIKEYBOOK2 ADIKEYPAGE2
2021/11/19 14:50:30
        Transaction Identifier  :       c6f0b82a557fe1e3c77484c188aa2978a7a5974bc7252fe33eb5577fabd4a290
        Tendermint Reference    :       1e47824134f333f8d3d0b9d84a413583a57ba3d9cede00d53462c58fb0e9f9ef
        Error code              :       ok
```

### Book

```bash
$ ./cli.exe book
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
$ ./cli.exe get ADITEST/ADIKEYBOOK1
        Height          Key Page Url
        1       :       acc://ADITEST/ADIKEYBOOK1
```

**Key Book Create**

```
Usage:
accumulate key book create [actor adi url] [signing key label] [key index (optional)] [key height (optional)] [new key book url] [key page url 1] ... [key page url n] Create new key page with 1 to N public keys
```

Example of usage:

```bash
$ ./cli.exe key book create ADITEST key1234 1 1 ADITEST/KEYBOOK1.1 ADITEST/KEYPAGE1.1 ADITEST/KEYPAGE1.2 ADITEST/KEYPAGE1.3
        Transaction Identifier  :       dd351321ca42568b9cc7e3a8faa88481e0e7e6759f4fd6b3976950b74865623a
        Tendermint Reference    :       71d231c0645a74c7ea21347bdcb54610e946f8a99eff0f48562634c14a928e27
        Error code              :       ok
```

### Completion

```bash
$ ./cli.exe completion
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

### Credits

Send credits using a lite account or adi key page to another lite account or adi key page

```bash
$ ./cli.exe credits
```

```
Usage:
  accumulate credits [actor lite account] [lite account or key page url] [amount]
  accumulate credits [actor url] [actor key name] [key index (optional)] [key height (optional)] [key page or lite account url] [amount]
```

Example of usage:

```bash
$ ./cli.exe credits acc://5a48d2999da25641db06a8e4baf54a275bfc6ed90cbcd21a/ACME acc://53948aeb1cda7cf854c6ec3104a66e336d26be1ad1790bb7/ACME 100
2021/12/02 20:58:43
        Transaction Identifier  :       4f8e7f98d0da08b1a3731f4a20e92e5a0a82f1b42e84958aff0eecc122d363af
        Tendermint Reference    :       dfd9d4b558c3abe05b93aa79f3e61190b180778269e37094d01ce1c4f48a354f
        Error code              :       ok
```


### Directory

Accumulate directory for Accumulate Digital Identifiers

```bash
$ ./cli.exe directory
```

```
Usage:
accumulate adi directory [url]              Get directory of sub-chains associate with a URL
```

Example of usage:

```bash
$ ./cli.exe adi directory ADITEST
        ADI Entries
        acc://ADITEST1/ssg0 (Key Book)
        acc://ADITEST1/sigspec0 (Key Page)

```

### Faucet

Faucet sends some TestNet ACME tokens to the requested anonymous token account.

```bash
$ ./cli.exe faucet
```

```bash
Usage:
faucet [url]               Get tokens from faucet to address
```

Example of usage:

```bash
$ ./cli.exe faucet acc://3ed6b2003242d2166508e117a2a66f8ca742b72e8d90d736/ACME
        Transaction Identifier  :       b72669697b6641f71595df9df0381599fdff5429171772d9f79e75533b7e5f57
        Tendermint Reference    :       36fde0e08fec2b123e8eb1876827d60be237e8b7c15ddb1505f4091bd4cba284
        Error code              :       ok
```

### Help

CLI Help

```bash
$ ./cli.exe help
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
  credits     Send credits to a recipient
  faucet      Get tokens from faucet
  get         Get data by URL
  help        Help about any command
  key         Create and manage Keys for ADI Key Books, and Pages
  page        Create and manage Keys, Books, and Pages
  tx          Create and get token txs
  version     get version of the accumulate node

Flags:
  -d, --debug              Print accumulated API calls
  -h, --help               help for accumulate
  -s, --server string      Accumulated server (default "https://testnet.accumulatenetwork.io/v1")
  -t, --timeout duration   Timeout for all API requests (i.e. 10s, 1m) (default 5s)

  Use "accumulate [command] --help" for more information about a command.
```

### Key

Managed the Keys, Key Pages, and Key Book for your Accumulate Digital

```bash
$ ./cli.exe key
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
$ ./cli.exe key generate key1234
key1234 :        e7f1541f7460fc38ef8ffeb5d483415074d68621b004614209d3d461d7abee12
```

**Key List**

```
Usage:
accumulate key list                   List generated keys associated with the wallet
```

Example of usage:

```bash
$ ./cli.exe key list
Public Key                                                              Key name
e7f1541f7460fc38ef8ffeb5d483415074d68621b004614209d3d461d7abee12        key1234
```

**Key Import Mnemonic**

```
Usage:
accumulate key import mnemonic [mnemonic phrase...]     Import the mnemonic phrase used to generate keys in the wallet
```

Example of Usage:

```bash
$ ./cli.exe key mnemonic humor demand lesson identify rookie road truth beef benefit thank camera tumble
Mnemonic imported
```

**Key Import Private Key**

```
Usage:
accumulate key import private [private key hex] [key name]      Import a key and give it a name in the wallet
```

Example of Usage:

```bash
$ ./cli.exe key import private c25288e8262fc23a5e8fc3acd523428b6913d05166f47022abef52acdba47930 benkey4
        name            :benkey4
        public key      :d5b57f10eb85a751094fcf943fc4997e45f0a90955294ca99cc5ee298d301690
```

**Key Export All**

```
Usage:
accumulate key export all                                 export all keys in wallet
```

Example of usage:

```bash
$ ./cli.exe key export all
name                    :       key101
        private key     :       23ab78aa778b044045e8287aca3347fe4e04d5060c5dbeb214661ef0bf2eec89
        public key      :       e086e27ff0bb5b146b6bdf55c8273211ddb62c684923502e22ef9d2d8b9a9ad5
name                    :       key102
        private key     :       7302b5758d15c5ef9eec4ba7182d3a18ba10776f8bb921945f3766028260b3f8
        public key      :       e7f1541f7460fc38ef8ffeb5d483415074d68621b004614209d3d461d7abee12
```

**Key Export Private**

```
Usage:
accumulate key export private [key name]                      export the private key by key name
```

Example of usage:

```bash
$ ./cli.exe key export private key1234
name                    :       key1234
        private key     :       7302b5758d15c5ef9eec4ba7182d3a18ba10776f8bb921945f3766028260b3f8
        public key      :       e7f1541f7460fc38ef8ffeb5d483415074d68621b004614209d3d461d7abee12
```

**Key Export Mnemonic**

```
Usage:
accumulate key export mnemonic                            export the mnemonic phrase if one was entered
```

Example of usage:

```bash
$ ./cli.exe key export mnemonic
mnemonic phrase: humor demand lesson identify rookie road truth beef benefit thank camera tumble
```

**Key Export Seed**

```
accumulate key export seed                       export the seed generated from the mnemonic phrase
```

Example of usage:

```bash
$ ./cli.exe key export seed
seed: b1310fcca7d5938d552561757d1e62a11a6fd3939cabdcfbbad94d1a6fb6a873f81b15f286ab4bed8e6139e4a6348387d555b72cf0e98793f5828264cfa78c77
```

### Page

```
$ ./cli.exe Page
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
$ ./cli.exe get ADITEST/ADIKEYPAGE1
        Index   Nonce   Public Key                                                              Key Name
        0       0       ec52b1f5b263010912431bf8e4af6ed84b3b3d64baff41b306fec359a512e7b5
```

**Key Page Create**

```
Usage:
accumulate key page create [actor adi url] [signing key label] [key index (optional)] [key height (optional)] [new key page url] [public key label 1] ... [public key label n] Create new key page with 1 to N public keys within the wallet
```

Example of usage:

```bash
$ ./cli.exe key page create ADITEST key1234 ADITEST/ADIKEYPAGE1.4 KEY1.4 KEY1.41 KEY1.42
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
}"
```

**Page Key Update**

```
accumulate key page update [key page url] [signing key label] [key index (optional)] [key height (optional)] [old key label] [new public key or label] Update key page with a new public key
```

Example of usage:

```bash
$ ./cli.exe page key update ADITEST/ADIKEYPAGE1 key5678 1 1 key5678 key1234
        Transaction Identifier  :       f61b5344e863141f25d34c2f40d8d1e2bd4cd29687c5f98822f91e9e39500682
        Tendermint Reference    :       2572c943abfc91b7e2192d9522657f5fffc8f4da1df55d5d0807ebca6f67faf7
        Error code              :       ok
```

**Page Key Add**

```
accumulate key page add [key page url] [signing key label] [key index (optional)] [key height (optional)] [new key label] Add key to key page
```

Example of usage:

```bash
$ ./cli.exe page key add ADITEST/ADIKEYPAGE1 key1234 1 1 key5678
        Transaction Identifier  :       f61b5344e863141f25d34c2f40d8d1e2bd4cd29687c5f98822f91e9e39500682
        Tendermint Reference    :       2572c943abfc91b7e2192d9522657f5fffc8f4da1df55d5d0807ebca6f67faf7
        Error code              :       ok
```

**Page Key Remove**

```
accumulate key page remove [key page url] [signing key label] [key index (optional)] [key height (optional)] [old key label] Remove key in key page
```

Example of usage:

```bash
$ ./cli.exe page key remove ADITEST/ADIKEYPAGE1 key1234 1 1 key1234
        Transaction Identifier  :       f61b5344e863141f25d34c2f40d8d1e2bd4cd29687c5f98822f91e9e39500682
        Tendermint Reference    :       2572c943abfc91b7e2192d9522657f5fffc8f4da1df55d5d0807ebca6f67faf7
        Error code              :       ok
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
$ ./cli.exe tx get 46469416c03b2b386e6c10da8e873f0d61392fc1e8384b63123d8d1e8a7326dd
{
   "data":{
      "from":"acc://7117c50f04f1254d56b704dc05298912deeb25dbc1d26ef6/ACME",
      "to":[
         {
            "amount":1000000000,
            "txid":"60d4c56055876cfa955721ff8613d9e372de02167951f360e4bcb27d2b1efb48",
            "url":"acc://e3f53a4582a9193914effacbd2ef5ad8105a61cdf78ee414/ACME"
         }
      ],
      "txid":"46469416c03b2b386e6c10da8e873f0d61392fc1e8384b63123d8d1e8a7326dd"
   },
   "keyPage":{
      "height":1,
      "index":0
   },
   "sig":"ce03ba0e52cdd4ce140de75f51727e2c40b1cc1f141e16916ad5f3a435935b81e99e43ce15274f973e1a06dab2dc174567f0544e1dfec39b516ef095fbf8670f",
   "signer":{
      "nonce":1635714053572291600,
      "publicKey":"d03c683332ed36add8d0eeb9eee9e2669b5565decec03acc43d762f3f79f49c2"
   },
   "sponsor":"acc://7117c50f04f1254d56b704dc05298912deeb25dbc1d26ef6/ACME",
   "status":{
      "code":"0"
   },
   "type":"tokenTx"
}
```

#### Tx Create

```
Usage:
accumulate tx create [from] [to] [amount]     Create new token tx
```

Example of usage:

```bash
$ ./cli.exe tx create acc://68fe2628a354d44ab349b08566ac35139a22b9896b1eff0d/ACME acc://78ef49e7ff69a7099774b72ec31edffb6c5a66a964aaa6e9/ACME 500000000
5917639ec8c66576b8e44797cfc198f0b85b0cbe4ab29ac8a1e8413a7b779f888d378ef83bcd38edf6023ed77a4e422059770da9d198ead8fd76245a353ced61
        Transaction Identifier  :       4a6683f35ac3191a482e606ac37e6224ef325936d045252af7bf7c5bd9970dfb
        Tendermint Reference    :       7745ebf61e42ee1b9e83b18a05125031d78f3bfdfe460e7be58f3c9296769e6a
        Error code              :       ok
```

#### Tx History

```
Usage:
accumulate tx history [url] [starting transaction number] [ending transaction number] Get transaction history
```

Example of usage:

```bash
$ ./cli.exe tx history acc://68fe2628a354d44ab349b08566ac35139a22b9896b1eff0d/ACME 0 1
{
   "data":[
      {
         "data":{
            "amount":"1000000000",
            "from":"acc://7117c50f04f1254d56b704dc05298912deeb25dbc1d26ef6/ACME",
            "to":"acc://68fe2628a354d44ab349b08566ac35139a22b9896b1eff0d/ACME",
            "tokenURL":"acc://ACME",
            "txid":"8aef025e2d4e90d75f703c51aae321e44eb26c2f79de0034ac7bb7aae4c00d94"
         },
         "keyPage":{
            "height":1,
            "index":0
         },
         "sig":"ef8d401dc1022131b5cc3083c3453cfb707fa68d06be47c584e9c38e8e04622f20afbddaba5e664595887483848dc109ca5492e0182686d2ac59c95710a23805",
         "signer":{
            "nonce":72,
            "publicKey":"7408e7dc62924a98b6c24fa814eec2d40363f9769875613d4d5ee04fdc1db94a"
         },
         "sponsor":"acc://7117c50f04f1254d56b704dc05298912deeb25dbc1d26ef6/ACME",
         "status":{
            "code":"0"
         },
         "type":"syntheticTokenDeposit"
      }
   ],
   "limit":1,
   "start":0,
   "total":2,
   "type":"tokenAccountHistory"
}
```
