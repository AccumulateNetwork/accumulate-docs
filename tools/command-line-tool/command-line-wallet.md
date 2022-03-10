# CLI Reference

The Command-Line Interface Tool allows you to interact with the Accumulate network and includes operations around token, identity, and key management. By default, the Command-Line Interface connects to the dedicated testnet server, but you can manually connect to a different server with `-s`

{% hint style="info" %}
If you'd like to connect to a specific testnet server, you can find a list of the available servers in the [Networks.go file](https://github.com/AccumulateNetwork/accumulated/blob/develop/networks/networks.go). Or you can use the public testnet server: `https://testnet.accumulatenetwork.io/v1`.
{% endhint %}

### Basic commands and flags

```bash
$ ./accumulate.exe
```

```bash
CLI for Accumulate Network

Usage:
  accumulate [command]

Available Commands
  account     Create and get token accounts
  adi         Create and manage ADI
  book        Manage key books for a ADI chains
  completion  generate the autocompletion script for the specified shell
  credits     Send credits to a recipient
  data        Create, add, and query adi data accounts
  faucet      Get tokens from faucet
  get         Get data by URL
  help        Help about any command
  key         Create and manage Keys for ADI Key Books, and Pages
  manager     add and remove manager from chain
  page        Create and manage Keys, Books, and Pages
  token       Issue and get tokens
  tx          Create and get token txs
  version     get version of the accumulate node

Flags:
  -d, --debug              Print accumulated API calls
  -h, --help               help for accumulate
  -j, --json               print outputs as json
      --no-wait            Do not wait for the transaction to complete
  -n, --pretend            Enables check-only mode for transactions
      --prove              Request a receipt proving the transaction is in a block
  -s, --server string      Accumulated server (default "https://testnet.accumulatenetwork.io/v2")
  -t, --timeout duration   Timeout for all API requests (i.e. 10s, 1m) (default 5s)
  -w, --wait duration      Wait for the transaction to complete


  Use "accumulate [command] --help" for more information about a command.
```

### Account

Create and get token accounts

```bash
$ ./accumulate.exe account
```

```bash
Usage:
  accumulate account [command]

Available Commands:
  create      Create an account
  generate    Generate random lite token account
  get         Get an account by URL
  list        Display all lite token accounts
  qr          Display QR code for lite account URL
  restore     Restore old lite token accounts

Flags:
  -h, --help   help for account

Global Flags:
  -d, --debug              Print accumulated API calls
  -j, --json               print outputs as json
  -n, --pretend            Enables check-only mode for transactions
      --prove              Request a receipt proving the transaction is in a block
  -s, --server string      Accumulated server (default "https://testnet.accumulatenetwork.io/v2")
  -t, --timeout duration   Timeout for all API requests (i.e. 10s, 1m) (default 5s)
```
**Account generate**

Generate random lite token account

```bash
Usage:
accumulate account generate                   
```

Example of usage:

```bash
$ ./accumulate.exe account generate
acc://26ddb87b5d12236f752680c97443a0212a93df4bdd7d784a/ACME :   3adc1fcd47c711e662b94335b1f270bd07bf27c279f65d5f754e091cc1e95b35
```

**Account get**

Get lite token account by URL

```bash
Usage:
accumulate account get [url]
```

Example of usage:

```bash
$ ./accumulate.exe account get acc://5a48d2999da25641db06a8e4baf54a275bfc6ed90cbcd21a/ACME
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
$ ./accumulate.exe get acc://ADITEST/TOKENS/ACME
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

#### Account list

Display all lite token accounts

```bash
Usage:
accumulate account list                       
```

Example of usage:

```bash
$ ./accumulate.exe account list
acc://68fe2628a354d44ab349b08566ac35139a22b9896b1eff0d/ACME
acc://78ef49e7ff69a7099774b72ec31edffb6c5a66a964aaa6e9/ACME
```

#### Account QR

Display QR code for lite account URL

```bash
Usage:
accumulate account qr [url]                   
```

Example of usage:

```bash
$ ./accumulate.exe account qr acc://f5a2c0416599ae08f264d1f55779540037bb7b8c85fe6bf5/ACME
█████████████████████████████████████
██ ▄▄▄▄▄ █▀    ▀█ ▄█▀ ▄ █ ▄█ ▄▄▄▄▄ ██
██ █   █ ██ ▀█▄▀█ ██▄▀▄█ ▀▀█ █   █ ██
██ █▄▄▄█ █▄▄▀▀▄▀▀██ █ █▀▄ ▄█ █▄▄▄█ ██
██▄▄▄▄▄▄▄█▄▀ █▄▀ █ ▀▄█▄▀ █▄█▄▄▄▄▄▄▄██
██ ▀▄▀▄▀▄███▄ ▄▄ ▄  ███  ███▀▀▄▀█▄▀██
████▀▄▄▄▄ ██▀▄▀▄█▀█▀▀▀▀  ▀▄█ ██▄██ ██
██ ▄▄▄ ▄▄▀█▀▄ ███▀▄ ▄█   █ █  █▀▀  ██
██  ▄█▄█▄   ▀▄ █ ▀▀ ██  ██▀▄▄▀▄ ▄▄▄██
███▀▄▄▄█▄█▄ ██ ▀▀██▄ █ ▄ ██  ██ ██ ██
██▀▀▄ ██▄  ▄█▄▄▀█▀  ▀▀█▀▄██▄ ▄▀ ██ ██
██▄██▄▄ ▄▄▄█  ▀  ▀ ▀███  ██   █▄█  ██
██▄▀▄ ▄█▄▀▄   ▄▀█▀▀ ▄▀▀▀▀█▄█▄▀▄ ▄▄ ██
██▄█▄█▄█▄█▀▀  ▀ ▀▄   █   ▀ ▄▄▄  ▀█▀██
██ ▄▄▄▄▄ ███ ▄█ ▄▀ ▀ ▀█▀▀▄ █▄█ ▀██▄██
██ █   █ █▄▄  ▄▄█▀ ▀█▄ ▄█▀  ▄  ██▄ ██
██ █▄▄▄█ █▄▄▀▀█████ ██ ▀ ▀  ██ ▀▄▀▄██
██▄▄▄▄▄▄▄█▄▄▄█▄████▄▄██▄▄▄▄██▄█▄█▄▄██
▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀
```

#### Account Create (ADI Token Account)

Create a token account for an ADI

```
Usage:
accumulate account create token [origin adi] [signing key name] [key index (optional)] [key height (optional)] [new token account url] [tokenUrl] [keyBookUrl]
```

Example of usage:

```bash
$ ./accumulate.exe account create token ADITEST key11 ADITEST/TOKENS acc://ACME acc://ADITEST/book0
        Transaction Id          :       9219c4aa063dbd4ad9a5ee02f3cca6e6445672a6f3b743aa6085239609b61d4a
        Tendermint Reference    :       9616826054dcc07d81e636ed185159249c0777ff27bf52ddae947371e0537f3d
        Error code              :       ok
        Error                   :       CheckTx
```

#### Account Create (ADI Data Account)

Create a data account under an ADI

```
Usage:
accumulate account create data [origin adi] [signing key name] [key index (optional)] [key height (optional)] [new data account url]  [keyBookUrl]
```

Example of usage:

```bash
$ ./accumulate.exe account create data ADITEST key11 ADITEST/DATA acc://ADITEST/book0
        Transaction Id          :       b9807394c46d41bcdb5fa6d500624fdb6a2832b50a34cd159c7d5d026584df38
        Tendermint Reference    :       aa090d8f31b863a5a0b5e313e4e6ab698b4a8762f1f16a6d24f673ccb501dc63
        Error code              :       ok
        Error                   :       CheckTx
```

### ADI

Create an Accumulate Digital Identifier. The Accumulate network is managed by an enhanced version of Distributed Digital Identities and Identifiers (DDIIs) that we refer to as Accumulate Digital Identifiers (ADIs).

```bash
$ ./accumulate.exe adi
```

```
Usage:
  accumulate adi [command]

Available Commands:
  create      Create new ADI
  directory   Get directory of URL's associated with an ADI with starting index and number of directories to receive
  get         Get existing ADI by URL
  list        Get existing ADI by URL

Flags:
  -h, --help   help for adi

Global Flags:
  -d, --debug              Print accumulated API calls
  -j, --json               print outputs as json
  -n, --pretend            Enables check-only mode for transactions
      --prove              Request a receipt proving the transaction is in a block
  -s, --server string      Accumulated server (default "https://testnet.accumulatenetwork.io/v2")
  -t, --timeout duration   Timeout for all API requests (i.e. 10s, 1m) (default 5s)

```

#### ADI create (Create New ADI from Lite Account)

```
Usage:
accumulate adi create [actor-lite-account] [adi url to create] [public-key or wallet key label] [key-book-name (optional)] [key-page-name (optional)]  Create new ADI from lite account
```

Example of usage:

```bash
$ ./accumulate.exe adi create acc://68fe2628a354d44ab349b08566ac35139a22b9896b1eff0d/ACME ADITEST key1234 ADIKEYBOOK1 ADIKEYPAGE1
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
$ ./accumulate.exe adi create ADITEST key1234 0 1 ADITEST2 key5678 ADIKEYBOOK2 ADIKEYPAGE2
2021/11/19 14:50:30
        Transaction Identifier  :       c6f0b82a557fe1e3c77484c188aa2978a7a5974bc7252fe33eb5577fabd4a290
        Tendermint Reference    :       1e47824134f333f8d3d0b9d84a413583a57ba3d9cede00d53462c58fb0e9f9ef
        Error code              :       ok
```

#### ADI directory

Get directory of URL's associated with an ADI with starting index and number of directories to receive

```bash
$ ./accumulate.exe adi directory
```

```
Usage:
accumulate adi directory [url]              Get directory of sub-chains associate with a URL
```

Example of usage:

```bash
$ ./accumulate.exe adi directory ADITEST
        ADI Entries
        acc://ADITEST1/ssg0 (Key Book)
        acc://ADITEST1/sigspec0 (Key Page)

```

#### ADI get

Get existing ADI by URL

```
Usage:
accumulate adi get [URL]                      
```

Example of usage:

```bash
        ADI Url         :       acc://ADITEST
        Key Book Url    :       acc://ADITEST/keybook1
```

#### ADI list

Get existing ADI list

```
Usage:
accumulate adi list                    
```

Example of usage:

```bash
        acc://ADITEST1     :       key11
        acc://adione       :       key61
        acc://aditwo       :       key51
        acc://aditthree    :       key61
```


### Book

```bash
$ ./accumulate.exe book
```

```
Usage:
accumulate book get [URL]                     Get existing Key Book by URL
accumulate book create [actor adi url] [signing key name] [key index (optional)] [key height (optional)] [new key book url] [key page url 1] ... [key page url n + 1] Create new key book and assign key pages 1 to N+1 to the book
```

Example usage:

```bash
accumulate book create acc://RedWagon redKey5 acc://RedWagon/RedBook acc://RedWagon/RedPage1
```

**Get Key Book**

Get existing Key Book by URL

```
Usage:
accumulate key get book [URL]                 
```

Example of usage:

```bash
$ ./accumulate.exe get ADITEST/ADIKEYBOOK1
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
$ ./accumulate.exe key book create ADITEST key1234 1 1 ADITEST/KEYBOOK1.1 ADITEST/KEYPAGE1.1 ADITEST/KEYPAGE1.2 ADITEST/KEYPAGE1.3
        Transaction Identifier  :       dd351321ca42568b9cc7e3a8faa88481e0e7e6759f4fd6b3976950b74865623a
        Tendermint Reference    :       71d231c0645a74c7ea21347bdcb54610e946f8a99eff0f48562634c14a928e27
        Error code              :       ok
```

### Completion

```
Usage:
Generate the autocompletion script for accumulate for the specified shell. See each sub-command's help for details on how to use the generated script.
```

```bash
$ ./accumulate.exe completion
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
  -j, --json               print outputs as json
  -n, --pretend            Enables check-only mode for transactions
  -s, --server string      Accumulated server (default "http://localhost:35554/v1")
  -t, --timeout duration   Timeout for all API requests (i.e. 10s, 1m) (default 5s)

Use "accumulate completion [command] --help" for more information about a command.
```

### Credits

Send credits using a lite account or adi key page to another lite account or adi key page

```bash
$ ./accumulate.exe credits
```

```
Usage:
  accumulate credits [origin lite account] [lite account or key page url] [amount]              
         Send credits using a lite account or adi key page to another lite account or adi key page
  accumulate credits [origin url] [origin key name] [key index (optional)] [key height (optional)] [key page or lite account url] [amount]              
         Send credits to another lite account or adi key page
```

Example of usage:

```bash
$ ./accumulate.exe credits acc://5a48d2999da25641db06a8e4baf54a275bfc6ed90cbcd21a/ACME acc://53948aeb1cda7cf854c6ec3104a66e336d26be1ad1790bb7/ACME 100
2021/12/02 20:58:43
        Transaction Identifier  :       4f8e7f98d0da08b1a3731f4a20e92e5a0a82f1b42e84958aff0eecc122d363af
        Tendermint Reference    :       dfd9d4b558c3abe05b93aa79f3e61190b180778269e37094d01ce1c4f48a354f
        Error code              :       ok
```

### Data

```bash
$ ./accumulate.exe data
```

```
  accumulate account create data [actor adi url] [signing key name] [key index (optional)] [key height (optional)] [adi data account url] [key book (optional)] 
         Create new data account
         example usage:  accumulate account create data acc://actor signingKeyName acc://actor/dataAccount acc://actor/book0
  
  accumulate account create data lite [lite token account] [name_0] ... [name_n] 
         Create new lite data account creating a chain based upon a name list
  accumulate account create data lite [origin url] [signing key name]  [key index (optional)] [key height (optional)] [name_0] ... [name_n] 
         Create new lite data account creating a chain based upon a name list
         example usage: accumulate account create data lite acc://actor signingKeyName example1 example2
  accumulate data get [DataAccountURL]                    
         Get existing Key Page by URL
  accumulate data get [DataAccountURL] [EntryHash]  
         Get data entry by entryHash in hex
  accumulate data get [DataAccountURL] [start index] [count] expand(optional) 
         Get a set of data entries starting from start and going to start+count, if "expand" is specified, data entries will also be provided 
  accumulate data write [data account url] [signingKey] [extid_0 optional)] ... [extid_n (optional)] [data] 
         Write entry to your data account. Note: extid's and data needs to be a quoted string or hex
   accumulate data write-to [account url] [signing key] [lite data account] [extid_0 (optional)] ... [extid_n (optional)] [data]
```

#### Create Data Account

Create new data account

```
Usage:
accumulate account create data [origin adi] [signing key name] [key index (optional)] [key height (optional)] [adi data account url]  [keyBookUrl]
```

Example of usage:

```bash
$ ./accumulate.exe account create data ADITEST key11 ADITEST/DATA acc://ADITEST/book0
        Transaction Id          :       b9807394c46d41bcdb5fa6d500624fdb6a2832b50a34cd159c7d5d026584df38
        Tendermint Reference    :       aa090d8f31b863a5a0b5e313e4e6ab698b4a8762f1f16a6d24f673ccb501dc63
        Error code              :       ok
        Error                   :       CheckTx
```

#### Create Data Lite Account

Create new lite data account creating a chain based upon a name list

```
Usage:
accumulate account create data lite [lite token account] [name_0] ... [name_n]
```

Example of usage:

```bash
$ ./accumulate.exe account create data lite acc://acf81a8d470f0ac2a085b4159da659ccf3a25681ab5f8257/ACME k01 k02
        Account Url             :acc://0401cc2a360c4685095bac0c751e3b2a6590c4663a46c33a

        Account Id              :0401cc2a360c4685095bac0c751e3b2a6590c466b33f63b9028f50d90c9fd13c
        Entry Hash              :a61b9a70ae0a12ac3c3ee5c2f3085be2e77848e6d2dcc0759ae94bd46a6ab1b6
        Transaction Hash        :       c6736b1f4bd11e4b546e2a1adef7e9c54256d6e3764a7a9d53eedc60bfa4d3db
        Envelope Hash           :       f80afa894e57472cfe395988705a3475c6f9c215f0ed43686db48294c9efb9b4
        Simple Hash             :       87cf3322eb18fd6ab2ea53f06287cd478e4e16d6ca33c9474b632816c3ed29a1
        Error code              :       ok
```

#### Get Data

Get existing Key Page by URL

```
Usage:
accumulate data get [DataAccountURL]

```

Example of usage:

```bash
$ ./accumulate.exe data get acc://ADITEST/DATA
{
   "type":"dataEntry",
   "merkleState":{
      "count":2,
      "roots":[
         null,
         "87c5cc4a4f86accac328b5773c3e6fe29e8af23cbaa5a14f154011e2e71af4d2"
      ]
   },
   "data":{
      "entry":{
         "data":"61646974776f64617461"
      },
      "entryHash":"b45fa53718dbc5bf31f2f6134d1ff84fe22b3760face9c2ab012fd66d16d1808"
   }
}
```

#### Get Data (entry hash)

Get data entry by entryHash in hex

```
Usage:
accumulate data get [DataAccountURL] [EntryHash]

```

Example of usage:

```bash
$ ./accumulate.exe data get acc://ADITEST/DATA b45fa53718dbc5bf31f2f6134d1ff84fe22b3760face9c2ab012fd66d16d1808
{
   "type":"dataEntry",
   "merkleState":{
      "count":2,
      "roots":[
         null,
         "87c5cc4a4f86accac328b5773c3e6fe29e8af23cbaa5a14f154011e2e71af4d2"
      ]
   },
   "data":{
      "entry":{
         "data":"61646974776f64617461"
      },
      "entryHash":"b45fa53718dbc5bf31f2f6134d1ff84fe22b3760face9c2ab012fd66d16d1808"
   }
}
```

#### Get Data (start & count)

Get a set of data entries starting from start and going to start+count, if "expand" is specified, data entries will also be provided

```
Usage:
accumulate data get [DataAccountURL] [start index] [count] expand(optional)

```

Example of usage:

```bash
$ ./accumulate.exe data get acc://ADITEST/DATA 0 1
{
   "type":"dataEntry",
   "merkleState":{
      "count":2,
      "roots":[
         null,
         "87c5cc4a4f86accac328b5773c3e6fe29e8af23cbaa5a14f154011e2e71af4d2"
      ]
   },
   "data":{
      "entry":{
         "data":"61646974776f64617461"
      },
      "entryHash":"b45fa53718dbc5bf31f2f6134d1ff84fe22b3760face9c2ab012fd66d16d1808"
   }
}
```
#### Data Write

Write entry to your data account.

```
Usage:
accumulate data write [data account url] [signingKey] [extid_0 optional)] ... [extid_n (optional)] [data]

```

Example of usage:

```bash
$ ./accumulate.exe data write acc://ADITEST/DATA key61 "testdata"
        Entry Hash              :       b45fa53718dbc5bf31f2f6134d1ff84fe22b3760face9c2ab012fd66d16d1808
        Transaction Id          :       513050cc0fb5459a27f7fd1661656d5c5b7fe3879740d51aabab0e072a0bb857
        Tendermint Reference    :       76821f50a8fa63fe6d74263754ad0c728003466d14822686963b604731225907
        Error code              :       ok
        Error                   :       CheckTx
```

#### Data Write-To

Write entry to your data account.

```
Usage:
accumulate data write-to [account url] [signing key] [lite data account] [extid_0 (optional)] ... [extid_n (optional)] [data]
```

Example of usage:

```bash
$ ./accumulate.exe data write-to acc://ADITEST key61 acc://08aecb75d3025d00bdc899e0ae675a6f03afc89d83e88879 testdata
        Account Url           :       acc://08aecb75d3025d00bdc899e0ae675a6f03afc89d83e88879
        Account Id            :       08aecb75d3025d00bdc899e0ae675a6f03afc89dde9836db705242e5b3355cce
        Entry Hash            :       89b9534d62d826478abb26cf53315dcefb49805471d226049ac1076f9269e6d1
        Transaction Hash      :       992af3be5221b8edca8b0252620f11d6b86720a9d5c005656d1f49a673ecac69
        Envelope Hash         :       afd6e529c7c215b15730270113b77f770d351d6d1444bbff0b181a8d454235ee
        Simple Hash           :       8e3fec17b992b01b4bc69e54a097a8b62ed6dabca9021fcc64ccadeb40abcf33
        Error code            :       ok
```

### Faucet

Faucet sends some TestNet ACME tokens to the requested anonymous token account.

```bash
$ ./accumulate.exe faucet
```

```bash
Usage:
faucet [url]               Get tokens from faucet to address
```

Example of usage:

```bash
$ ./accumulate.exe faucet acc://3ed6b2003242d2166508e117a2a66f8ca742b72e8d90d736/ACME
        Transaction Identifier  :       b72669697b6641f71595df9df0381599fdff5429171772d9f79e75533b7e5f57
        Tendermint Reference    :       36fde0e08fec2b123e8eb1876827d60be237e8b7c15ddb1505f4091bd4cba284
        Error code              :       ok
```

### Help

CLI Help

```bash
$ ./accumulate.exe help
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
  data        Create, add, and query adi data accounts
  faucet      Get tokens from faucet
  get         Get data by URL
  help        Help about any command
  key         Create and manage Keys for ADI Key Books, and Pages
  page        Create and manage Keys, Books, and Pages
  token       Issue and get tokens
  tx          Create and get token txs
  version     get version of the accumulate node

Flags:
  -d, --debug              Print accumulated API calls
  -h, --help               help for accumulate
  -j, --json               print outputs as json
  -n, --pretend            Enables check-only mode for transactions
  -s, --server string      Accumulated server (default "https://testnet.accumulatenetwork.io/v1")
  -t, --timeout duration   Timeout for all API requests (i.e. 10s, 1m) (default 5s)

  Use "accumulate [command] --help" for more information about a command.
```

### Key

Managed the Keys, Key Pages, and Key Book for your Accumulate Digital

```bash
$ ./accumulate.exe key
```

```
  Usage:
  accumulate key generate [key name]     Generate a new key and give it a name in the wallet
  accumulate key list                   List generated keys associated with the wallet
  accumulate key import mnemonic [mnemonic phrase...]     Import the mneumonic phrase used to generate keys in the wallet
  accumulate key import private [private key hex] [key name]      Import a key and give it a name in the wallet
  accumulate key import lite [private key hex]      Import a key as an anonymous address
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
$ ./accumulate.exe key generate key1234
key1234 :        e7f1541f7460fc38ef8ffeb5d483415074d68621b004614209d3d461d7abee12
```

**Key List**

```
Usage:
accumulate key list                   List generated keys associated with the wallet
```

Example of usage:

```bash
$ ./accumulate.exe key list
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
$ ./accumulate.exe key mnemonic humor demand lesson identify rookie road truth beef benefit thank camera tumble
Mnemonic imported
```

**Key Import Private Key**

```
Usage:
accumulate key import private [private key hex] [key name]      Import a key and give it a name in the wallet
```

Example of Usage:

```bash
$ ./accumulate.exe key import private c25288e8262fc23a5e8fc3acd523428b6913d05166f47022abef52acdba47930 benkey4
        name            :benkey4
        public key      :d5b57f10eb85a751094fcf943fc4997e45f0a90955294ca99cc5ee298d301690
```

**Key Import Lite**

```
Usage:
accumulate key import lite [private key hex]      Import a key as an anonymous address
```

Example of Usage:

```bash
$ ./accumulate.exe key import lite 52693a08f2511ecd05b41e0ea6e6b6f2b7dee4248293b8c4ae9e4aacb8f3ae54
        name            :acc://4111d56848824a2d74ee93e2c42091f7019a87c7649b48fe/ACME
        public key      :76324e43a382e6ff6a9724f8dae137b93f5d5a61a3eb9d6e5213739b656c5d44
```

**Key Export All**

```
Usage:
accumulate key export all                                 export all keys in wallet
```

Example of usage:

```bash
$ ./accumulate.exe key export all
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
$ ./accumulate.exe key export private key1234
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
$ ./accumulate.exe key export mnemonic
mnemonic phrase: humor demand lesson identify rookie road truth beef benefit thank camera tumble
```

**Key Export Seed**

```
accumulate key export seed                       export the seed generated from the mnemonic phrase
```

Example of usage:

```bash
$ ./accumulate.exe key export seed
seed: b1310fcca7d5938d552561757d1e62a11a6fd3939cabdcfbbad94d1a6fb6a873f81b15f286ab4bed8e6139e4a6348387d555b72cf0e98793f5828264cfa78c77
```

### Manager

**Update Manager**

```
Usage:
accumulate manager set [key page url] [signing key name] [key book url]                
```

Example of usage:

```bash
$ ./accumulate manager set ADITEST/page keytest ADITEST/book
        Transaction Hash        :       6b0e7de9b549823623e2ac019442e415968a892d602b91c04390acfb641c51f4
        Envelope Hash           :       227b322acda0564b6ef7d6753e7cf1442df689fdc84b8659b3b6c2ce52af259b
        Simple Hash             :       cc8af739ecabaa116f7484000cd8b9ff8d0065672a9b7b17d59ea742e5e5b4d5
        Error code              :       ok
```

**Remove Manager**

```
accumulate manager remove  [key page url] [signing key name]                      
```

Example of usage:

```bash
$ ./accumulate manager remove ADITEST/page keytest
        Transaction Hash        :       1ec19ab6084c1e82632a3c441de82a4ddb659afc3b40dda365510e07465f080d
        Envelope Hash           :       53ca879b1dc6bac8899d5bf70657dd9af4f027f87000cd5673c1b40b62b7d425
        Simple Hash             :       4cbe000690b7eb27d669584e28497403dae7539864bf030dc178b559dcb58a90
        Error code              :       ok
```


### Page

```
$ ./accumulate.exe page
```

```
accumulate page create [actor adi url] [signing key name] [key index (optional)] [key height (optional)] [new key page url] [public key 1] ... [public key hex or label n + 1] 
            Create new key page with 1 to N+1 public keys 
            example usage: accumulate key page create acc://RedWagon redKey5 acc://RedWagon/RedPage1 redKey1 redKey2 redKey3
  accumulate page get [URL]                     
            Get existing Key Page by URL
  accumulate page key update [key page url] [signing key name] [key index (optional)] [key height (optional)] [old key label] [new public key or label] 
            Update key in a key page with a new public key
            example usage: accumulate page key update  acc://RedWagon/RedPage1 redKey1 redKey2 redKey3
  accumulate page key add [key page url] [signing key name] [key index (optional)] [key height (optional)] [new key label] 
            Add key to a key page
            example usage: accumulate page key add acc://RedWagon/RedPage1 redKey1 redKey2
  accumulate page key remove [key page url] [signing key name] [key index (optional)] [key height (optional)] [old key label] 
            Remove key from a key page
            example usage: accumulate page key remove acc://RedWagon/RedPage1 redKey1 redKey2 
```

**Get Key Page**

Get existing Key Page by URL

```
Usage:
accumulate key get page [URL]                 
```

Example of usage:

```bash
$ ./accumulate.exe get ADITEST/ADIKEYPAGE1
        Index   Nonce   Public Key                                                              Key Name
        0       0       ec52b1f5b263010912431bf8e4af6ed84b3b3d64baff41b306fec359a512e7b5
```

**Key Page Create**

Create new key page with 1 to N public keys within the wallet

```
Usage:
accumulate key page create [actor adi url] [signing key label] [key index (optional)] [key height (optional)] [new key page url] [public key label 1] ... [public key label n] 
```

Example of usage:

```bash
$ ./accumulate.exe key page create ADITEST key1234 ADITEST/ADIKEYPAGE1.4 KEY1.4 KEY1.41 KEY1.42
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

Update key page with a new public key

```
Usage:
accumulate key page update [key page url] [signing key label] [key index (optional)] [key height (optional)] [old key label] [new public key or label] 
```

Example of usage:

```bash
$ ./accumulate.exe page key update ADITEST/ADIKEYPAGE1 key5678 1 1 key5678 key1234
        Transaction Identifier  :       f61b5344e863141f25d34c2f40d8d1e2bd4cd29687c5f98822f91e9e39500682
        Tendermint Reference    :       2572c943abfc91b7e2192d9522657f5fffc8f4da1df55d5d0807ebca6f67faf7
        Error code              :       ok
```

**Page Key Add**

Add key to key page

```
accumulate key page add [key page url] [signing key label] [key index (optional)] [key height (optional)] [new key label] 
```

Example of usage:

```bash
$ ./accumulate.exe page key add ADITEST/ADIKEYPAGE1 key1234 1 1 key5678
        Transaction Identifier  :       f61b5344e863141f25d34c2f40d8d1e2bd4cd29687c5f98822f91e9e39500682
        Tendermint Reference    :       2572c943abfc91b7e2192d9522657f5fffc8f4da1df55d5d0807ebca6f67faf7
        Error code              :       ok
```

**Page Key Remove**

Remove key in key page

```
accumulate key page remove [key page url] [signing key label] [key index (optional)] [key height (optional)] [old key label] 
```

Example of usage:

```bash
$ ./accumulate.exe page key remove ADITEST/ADIKEYPAGE1 key1234 1 1 key1234
        Transaction Identifier  :       f61b5344e863141f25d34c2f40d8d1e2bd4cd29687c5f98822f91e9e39500682
        Tendermint Reference    :       2572c943abfc91b7e2192d9522657f5fffc8f4da1df55d5d0807ebca6f67faf7
        Error code              :       ok
```

### Token

```bash
$ ./accumulate.exe token
```

```bash
Usage:
  burn        burn tokens
  create      Create new token
  get         get token by URL
  issue       send tokens from a token url to a recipient
```

#### Token Burn

Burn Tokens

```
Usage:
 accumulate token burn [adi or lite token account] [adi signer key name (if applicable)] [amount] [flags]     
```

Example of usage:

```bash
./accumulate token burn acc://09bca3fcd7e28434f4fb5a3c7317d64e955acbc102e45df5/ACME 1

        Transaction Hash        :       a6d7f5aa0c373c6888adba7e3c84df0b3c5b2688427df420c4c749cf452a5864
        Envelope Hash           :       b0a58ed58f096cf35a50eda7fcb728fa0a7d9129d5e061d03071fa1a00d927ba
        Simple Hash             :       0f5d6fa9ba05d322487ce35db53a5f69d0e1bc0f52c3bbd972cb2cde88042b37
        Error code              :       ok
```

#### Token Create

Create new token

```
Usage:
accumulate token create [origin adi url] [signer key name] [url] [symbol] [precision] [properties]     
```

Example of usage:

```bash
./accumulate token create acc://ADITEST key11 acc://ADITEST/TokenTest ADT 2

        Transaction Hash        :       42b9cc80cd430a3dcf759e43190192b358743b42d4f80d4c6367e7b36b90a364
        Envelope Hash           :       e72f8b6561dda8531a2fd3c58317bc35e4300e9953762f662a0b5a0ee4392a4f
        Simple Hash             :       e8bd622ebe235c99e799e6780f42f8cae6248211a62303086cea82a9bbbeca0d
        Error code              :       ok
```

#### Token Get

Get token by URL

```
Usage:
accumulate token get [url]     
```

Example of usage:

```bash
./accumulate token get acc://ADITEST/TokenTest

        Token URL       :       acc://ADITEST/TokenTest
        Symbol          :       ADT
        Precision       :       2
        Supply          :       0
        Supply Limit    :       no
        Properties URL  :
```

#### Token Issue

Send tokens from a token url to a recipient

```
Usage:
accumulate token issue [adi token url] [signer key name] [recipient url] [amount] [flags]     
```

Example of usage:

```bash
./accumulate token issue acc://fun/funtoken kgkey acc://09bca3fcd7e28434f4fb5a3c7317d64e955acbc102e45df5/ACME 1

        Transaction Hash        :       a2c232565b3b9864740966b17a97a14560e8a9bbf2cbf362928a113e2435a4af
        Envelope Hash           :       2b40effc2cb9edc6edc7dfc7482684a487a100dc485469bc5f4e376181f0f6c0
        Simple Hash             :       7d8197f93f3f361be3dbc92dd0ac8bd7cd51da2b1ec28f25ce7ae3d4db6de7ae
        Error code              :       ok
```

### Tx

Send token from one anonymous token account to another one.

```bash
$ ./accumulate.exe tx
```

```bash
Usage:
  accumulate tx get [txid]                      
         Get token transaction by txid
  accumulate tx create [from] [to] [amount]     
         Create new token tx
  accumulate tx execute [from] [payload]        
         Execute an arbitrary transaction
  accumulate tx sign [origin] [signing key name] [key index (optional)] [key height (optional)] [txid]  
         Sign a pending transaction
  accumulate tx history [url] [starting transaction number] [ending transaction number] 
         Get transaction history
  accumulate tx pending [txid]                  
         Get token transaction by txid
  accumulate tx pending [height]                        
         Get token transaction by block height
  accumulate tx pending [starting transaction number]   [ending transaction number]             
         Get token transaction by block height
 
```

#### Tx Get

Get token transaction by txid

```
Usage:
accumulate tx get [txid]                      
```

Example of usage:

```shell
$ ./accumulate.exe tx get 46469416c03b2b386e6c10da8e873f0d61392fc1e8384b63123d8d1e8a7326dd
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

Create new token tx

```
Usage:
accumulate tx create [from] [to] [amount]     
```

Example of usage:

```bash
$ ./accumulate.exe tx create acc://68fe2628a354d44ab349b08566ac35139a22b9896b1eff0d/ACME acc://78ef49e7ff69a7099774b72ec31edffb6c5a66a964aaa6e9/ACME 500000000

        Transaction Identifier  :       4a6683f35ac3191a482e606ac37e6224ef325936d045252af7bf7c5bd9970dfb
        Tendermint Reference    :       7745ebf61e42ee1b9e83b18a05125031d78f3bfdfe460e7be58f3c9296769e6a
        Error code              :       ok
```

#### Tx Create (between ADI token accounts)

Send tokens between ADI token accounts.

```
Usage:
accumulate tx create [from] [to] [amount]    
```

Example of usage:

```bash
$ ./accumulate.exe tx create acc://adione/one key61 acc://adithree/three  0.5

        Transaction Identifier  :       73fc83c76f36a6a1850e84d2149223de69903c5c635be64ef234d61f8929b4ae
        Tendermint Reference    :       b981ef488248ad3adf4b799a4b717e9f8026b0b8f6e162fa992b26ba68777385
        Error code              :       ok
        Error                   :       CheckTx
```

#### Tx Execute

Execute an arbitrary transaction

```
Usage:
accumulate tx execute [from] [payload]
```

Example of usage:

```bash
$ ./accumulate tx execute acc://ADITEST key1 '{"type": "createTokenAccount", "url": "acc://ADITEST/tokn", "tokenUrl": "acc://ACME"}'

        Transaction Hash        :       ab1031b05c5c5800354fc42c5d0d96f1f4e03c67248e97a3d24d0c255d574cf5
        Envelope Hash           :       37fe7276d368c0228acfcc1b646a02bf0b696b4b83707abbf986ce2dcd550a33
        Simple Hash             :       458cc577e82bc7ec2240dce06e4ec66d03bba8246b977dff486366e774fef581
        Error code              :       ok
```

#### Tx Sign

Sign a pending transaction

```
Usage:
accumulate tx sign [origin] [signing key name] [key index (optional)] [key height (optional)] [txid]
```

Example of usage:

```bash
$ ./accumulate tx sign ADITEST/testtoken key2 fa3aac0886f345ec32b5762277de2a6645b6d8ac5551e7aa0761e41e80a7726b

        Transaction Hash        :       fa3aac0886f345ec32b5762277de2a6645b6d8ac5551e7aa0761e41e80a7726b
        Envelope Hash           :       87d9a4019c019267e6a1f452e7119ab4cb9bd300827f41b84ce56e31a9acb7be
        Simple Hash             :       1d5f884c4cde73d3b561a9ebe6cc9909fce6435220cf2644bd2925fa3cff6367
        Error code              :       ok
```

#### Tx History

Get transaction history

```
Usage:
accumulate tx history [url] [starting transaction number] [ending transaction number] 
```

Example of usage:

```bash
$ ./accumulate.exe tx history acc://68fe2628a354d44ab349b08566ac35139a22b9896b1eff0d/ACME 0 1
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

#### Tx Pending

Get token transaction by txid

```
Usage:
accumulate tx pending [txid]
```

Example of usage:

```bash
$ ./accumulate.exe tx pending b5ca6c9ed9aa092637236f73533a8579bb072fadecf9fac1b777b43aad545fe3

        Pending Tranactions -> Start: 0  Count: 0        Total: 0
``` 

Get token transaction by block height

```
Usage:
accumulate tx pending [height]
```

Example of usage:

```bash
$ ./accumulate.exe tx pending 1

        Pending Tranactions -> Start: 0  Count: 0        Total: 0
``` 

Get token transaction by beginning and ending height

```
Usage:
accumulate tx pending [starting transaction number]   [ending transaction number]
```

Example of usage:

```bash
$ ./accumulate.exe tx pending fa3aac0886f345ec32b5762277de2a6645b6d8ac5551e7aa0761e41e80a7726b 

        Pending Tranactions -> Start: 0  Count: 0        Total: 0
``` 

#### Scratch Token Account

Create new scratch token account

Example of usage:

```bash
$ ./accumulate tx execute acc://ADITEST key11 '{"type": "createTokenAccount", "url": "acc://ADITEST/tokn", "tokenUrl": "acc://ACME", "scratch": true}'

        Transaction Hash        :       ab1031b05c5c5800354fc42c5d0d96f1f4e03c67248e97a3d24d0c255d574cf5
        Envelope Hash           :       37fe7276d368c0228acfcc1b646a02bf0b696b4b83707abbf986ce2dcd550a33
        Simple Hash             :       458cc577e82bc7ec2240dce06e4ec66d03bba8246b977dff486366e774fef581
        Error code              :       ok
```

#### Scratch Data Account

Create new scratch data account

Example of usage:

```bash
$ ./accumulate tx execute acc://ADITEST key11 '{"type": "createDataAccount", "url": "acc://ADITEST/data", "scratch": true}'

        Transaction Hash        :       6643103744814c1671c451115cf66299b2bebcf4ea97b498f94169181386d924
        Envelope Hash           :       fce3d26fcf78d2e144e0d8ee3f2fd69303655549fd223bc1bd4a95a0101d47d3
        Simple Hash             :       924e43967cc24048d51f02daa4f9e20902b0516a12b210de131ded16f3959e29
        Error code              :       ok
```