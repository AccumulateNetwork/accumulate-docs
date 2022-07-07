---
description: All the commands available via the Command Line Tool are documented below
---

# CLI Reference

&#x20;

Account Types:

•       Lite Identity

•       Lite Token Account

•       Lite Data Account

•       Accumulate Digital Identifier (ADI)

•       Key Book

•       Key Page

•       ADI Token Account

•       ADI Data Account

•       Token Issuer Account

•       Sub-ADIs

•       Sub-Sub-ADIs

Credits are technically not an account type but will be explained below.

&#x20;

**Lite Identities and Lite Token Accounts**

A Lite Token Account is the most basic token Account in Accumulate. Credits for a Lite Token Account are stored in the Lite Token Account’s Lite Identity Account. A Lite Identity’s address is the same as the Lite Token Accounts address without ‘/ACME’ at the end. The ‘ACME’ denotes the type of token the Lite Token Account holds. ACME is the native token to the Accumulate Protocol.

Lite Token Account: acc://1080be6dc3895faccb614470fc4320a99d7ba04ec77fab1f/ACME\
Lite Identity Account: acc://1080be6dc3895faccb614470fc4320a99d7ba04ec77fab1f

There are multiple signature types that can be used to create a Lite Identity and Lite Token Account such as ED25519, Bitcoin and Ethereum Signatures, and RCD1 which supports Factom Accounts. Factoid Addresses from the Factom Protocol will convert into Accumulate Lite Token Accounts.

Constructing a Lite Token Account or Lite Identity Account address locally will not create the account. The protocol will only recognize its creation when ACME is added to the Lite Token Account, or Credits are added to the Lite Identity. On the Testnet, a Faucet can be used to generate test ACME. The Faucet only works with ACME Lite Token Accounts. Once the Accumulate Protocol MainNet is live, ACME can be purchased through an exchange.

Each Lite Token Account can only hold one type of token. To create a Lite Token Account that can hold a custom token, a Token Issuer Account, which will be explained later, replaces ‘ACME’ in the Lite Token Account’s Address. The Token Issuer Account defines the token type and it’s properties. A Lite Identity’s credits reserves are used both from ACME Lite Token Accounts and Lite Token Accounts that hold custom Tokens.

Other Token Accounts which exist within Accumulate are Accumulate Digital Identifier (ADI) Token Accounts, which can also hold ACME and whereby a separate Token Accounts within the same ADI can hold custom tokens and Sub-ADI Token Accounts. Both of which will be explained in later sections. Any Token Account can send tokens to another Token Account type as long as the token type is the same.

&#x20;

&#x20;****&#x20;

**Lite Token Account/Lite Identity Creation**

./accumulate account generate

&#x20;

```shell-session
lite identity        :       0143b52490530b90eef9b1a2405e322c6badc1e90e200c56
lite token account    :       acc://0143b52490530b90eef9b1a2405e322c6badc1e90e200c56/ACME
public key      :       03c633851507f63ef8517dc934075f2abe2f8c3b3053b5a49a477e8513e01955
key type        :       ed25519
```

&#x20;

**Account List**

**./accumulate account list**

&#x20;       key name                :       001846c0a1590675fd0ad816ab4873387ef127cd9b307c24

&#x20;       lite account    :       acc://001846c0a1590675fd0ad816ab4873387ef127cd9b307c24/ACME

&#x20;       public key      :       3615e429b89fa3d6b636412d7a17b13cc321c14b2f2e5bf520868c9617401845

&#x20;       key type        :       legacyED25519

&#x20;

&#x20;       key name                :       003df7b8b865b3eda520dbb224eaf7536ee98cc25874ce54

&#x20;       lite account    :       acc://003df7b8b865b3eda520dbb224eaf7536ee98cc25874ce54/ACME

&#x20;       public key      :       45090e7cfa0edd52db7181fa0a30f1da8d2c0b1bdc6b4847de75fe922ad9e755

&#x20;       key type        :       ed25519

&#x20;

**Faucet Transaction**

The Test Faucet can be used to add test ACME tokens to a Lite Token Account. The Sponsor of the transaction is the Test Faucet address that holds Test ACME. ([acc://7117c50f04f1254d56b704dc05298912deeb25dbc1d26ef6/ACME](https://beta.explorer.accumulatenetwork.io/acc/7117c50f04f1254d56b704dc05298912deeb25dbc1d26ef6/ACME)):

&#x20; accumulate faucet \[url]               Get tokens from faucet to address

&#x20;****&#x20;

./accumulate faucet acc://0143b52490530b90eef9b1a2405e322c6badc1e90e200c56/ACME

&#x20;       Transaction Hash        : a0018d18c558c36f3f639fa1a64e2e9c47cc705fdf0d3f65a8ec8f0e0bd0f328

&#x20;       Signature 0 Hash        : 78d521b36691c46216a66d6648dd620a9f6ec312a24b3b0f29a9889887f4953d

&#x20;       Simple Hash             : ab039db9714e8a30b0443054dea78a36e754ead8ca50a6ab6e50adc62ef3d801

&#x20;       Error code              : ok

&#x20;       Result                  :

&#x20;

_**The Transaction Hash is a hash of the transaction without signatures and the Signature Hash is the Transaction Hash with the Signature appended to it and hashed.**_

&#x20;

**TX Get Transaction Hash (TXID)**

To query a transaction by the transaction ID a tx get command is required:

&#x20;

&#x20; accumulate tx get \[txid]                      Get token transaction by txid

&#x20;

accumulate tx get a0018d18c558c36f3f639fa1a64e2e9c47cc705fdf0d3f65a8ec8f0e0bd0f328

&#x20;  (type): Acme Faucet

&#x20;  Transaction Type: acme Faucet

&#x20;  Url: acc://0143b52490530b90eef9b1a2405e322c6badc1e90e200c56/ACME

&#x20; \- Synthetic Transaction 0 : 8eb0088ec37e2fca37fd915aa2348e03b30c77e2b2abdcbc4ee7b94e6c532f2f&#x20;

&#x20;

**TX Get Signature Hash**

To query the transaction hash from the Faucet account transaction:

&#x20;

&#x20; accumulate tx get \[txid]                      Get token transaction by txid

&#x20;

./accumulate tx get 78d521b36691c46216a66d6648dd620a9f6ec312a24b3b0f29a9889887f4953d

&#x20;  (type): Acme Faucet

&#x20;  Transaction Type: acme Faucet

&#x20;  Url: acc://0143b52490530b90eef9b1a2405e322c6badc1e90e200c56/ACME

&#x20; \- Synthetic Transaction 0 : 8eb0088ec37e2fca37fd915aa2348e03b30c77e2b2abdcbc4ee7b

&#x20;

94e6c532f2f

&#x20;

**Synthetic TX Get**

To query the synthetic transaction from the Faucet Account transaction:

&#x20; accumulate tx get \[txid]                      Get token transaction by txid

&#x20;

./accumulate tx get 8eb0088ec37e2fca37fd915aa2348e03b30c77e2b2abdcbc4ee7b94e6c532f2f

Receive 2000000.00000000 ACME to acc://0143b52490530b90eef9b1a2405e322c6badc1e90e200c56/ACME (cause: A0018D18C558C36F3F639FA1A64E2E9C47CC705FDF0D3F65A8EC8F0E0BD0F328)

\---

&#x20; \- Transaction           : 8eb0088ec37e2fca37fd915aa2348e03b30c77e2b2abdcbc4ee7b94e6c532f2f

&#x20; \- Signer Url            : acc://0143b52490530b90eef9b1a2405e322c6badc1e90e200c56/ACME

&#x20; \- Signatures            :

&#x20;   \- Signer              : acc://bvn-BVN0/validators/1 (keyPage)

&#x20;     \-                   : synthetic

&#x20;     \-                   : 739d02db90d8f4a979241d37aab8de104f7d967cfc29611e8664afb70006aa4e0b6d728c9d01a8481704e7a3a0b17ce15de6c7744d82508e9102ac3572cbdf0e (sig)

&#x20;     \-                   : b4449beb71f752736e8223fae4a407037e3016e7e91d5b2dc60e87f5b2978cc4 (key hash)

&#x20;     \-                   : receipt

&#x20; \- Signatures            :

&#x20;   \- Signer              : acc://dn/validators/1 (unknownSigner)

&#x20;     \-                   : receipt

&#x20;

**Get Token Balance**

To check the token balance of a Lite Token Account a Get function will query the balance. The Token URL in the output specifies the type of Token.

&#x20;****&#x20;

accumulate get \[url]          Get data by Accumulate URL

&#x20;

./accumulate get acc://0143b52490530b90eef9b1a2405e322c6badc1e90e200c56/ACME &#x20;

&#x20;

&#x20;       Account Url     :       acc://0143b52490530b90eef9b1a2405e322c6badc1e90e200c56/ACME

&#x20;       Token Url       :       acc://ACME

&#x20;       Balance         :       2000000.00000000 ACME

&#x20;

&#x20;

**Key Generation**

A named key can be generated using the key generate function. This will also output the name of the public key as well and key type. Unless specified otherwise this will create an ed25519 key.

&#x20;

./accumulate key generate keytest

&#x20;       name            :       keytest

&#x20;       lite account    :       acc://601b40a84a69f216173a457c44de5b942bf5aec62a7003ce/ACME

&#x20;       public key      :       1ac021a5d6a1e457102019d5fd00cc04d3e9783a745905761d3fab96e9598c57

&#x20;       key type        :       ed25519

&#x20;

To generate named keys of other signature types this can be explicitly referenced. A Lite Token Account/Lite Identity are produced as well as the public key of the specified key type. When assets are bridged over from other protocols, they can maintain the security of the protocol they originated from.

&#x20;****&#x20;

**Bitcoin:**

./accumulate key generate --sigtype btc testbtc

&#x20;       name            :       testbtc

&#x20;       lite account    :       acc://321ec96337292b2a34b6b5c8c62f54f1d198465b0a00f35a/ACME

&#x20;       public key      :       0396adeb7869b780606a8fe1218ebfb9c71e7e91ca72b1d95210717c3ed5f4dfd8

&#x20;       key type        :       btc

&#x20;****&#x20;

**Bitcoin Legacy:**

./accumulate key generate --sigtype btclegacy testbtclegacy

&#x20;       name            :       testbtclegacy

&#x20;       lite account    :       acc://95b9e649f8853e40c59aea635ef883100f014b85d57b75a6/ACME

&#x20;       public key      :       040ea7496cd6f50c77230d89b9c9ca60bca1d078b06e0efba9c5f3068f8668d229a38fdb71105cb4beffe66958c9b46bec940296346c494a65263f1330c4340755

&#x20;       key type        :       btclegacy

&#x20;****&#x20;

**Ethereum:**

./accumulate key generate --sigtype eth testeth

&#x20;       name            :       testeth

&#x20;       lite account    :       acc://388acd64ebbabbf89f0c2b250fb181ef5dff5122b1448c87/ACME

&#x20;       public key      :       041901c4486b91f82d16281d84031bd25baf2d61703a3c4caade2f5a844a6f73f2f1e2f80f995fa9db6ed794234eb5efdd44efad81a4b2bf6e14319bd74b55d588

&#x20;       key type        :       eth

&#x20;****&#x20;

**Factom (RCD1)**

./accumulate key generate --sigtype RCD1 testRCD1

&#x20;       name            :       testRCD1

&#x20;       lite account    :       acc://6a3956d856638d58757e0a47f24fa112876e664ffa322fa2/ACME

&#x20;       public key      :       9f3d2d2604d8e50453f59d379c25c0fc5220d512a786f3c419947e6050e758a6

&#x20;       key type        :       rcd1

&#x20;****&#x20;

**Key Import Mnemonic**

accumulate key import mnemonic \[mnemonic phrase...] Import the mnemonic phrase used to generate keys in the wallet

&#x20;

./accumulate key import mnemonic decide trap aisle raise above wool excite funny tuna body choice stereo

mnemonic import successful

&#x20;

**Key Import Private Key**

accumulate key import private \[private key hex] \[key name] Import a key and give it a name in the wallet

&#x20;

./accumulate key import private c25288e8262fc23a5e8fc3acd523428b6913d05166f47022abef52acdba47930 Key5

name : Key5

lite account : acc://0d83eababd1ba323f69470576f8c9eb563821a075c4e627d/ACME

public key : d5b57f10eb85a751094fcf943fc4997e45f0a90955294ca99cc5ee298d301690

key type : ed25519

&#x20;

**Key Import Factoid**

accumulate key import factoid \[factoid private address] Import a factoid private address

&#x20;

./accumulate key import factoid Fs23yok1z8ZsHtoMsWc1oMy76sKRgHF3jN6HLjoMQ9iMxYrnnkiL

name : FA2MSMBiyHmBLP1LDYAVWGRkkLpr64mMMi7N11hKchT6bAi926XW

lite account : acc://32c484ebfd344810353cb273d538166f3b4a9391486343d5/ACME

public key : aba7ecaa24874d13f272b87b7924bc4613a82904a98ef399f4b6d9a29e46a381

key type : rcd1

&#x20;

**Key Import Lite**

accumulate key import lite \[private key hex] Import a key as an anonymous address

&#x20;

./accumulate key import lite 52693a08f2511ecd05b41e0ea6e6b6f2b7dee4248293b8c4ae9e4aacb8f3ae54

name : 4111d56848824a2d74ee93e2c42091f7019a87c7649b48fe

lite account : acc://4111d56848824a2d74ee93e2c42091f7019a87c7649b48fe/ACME

public key : 76324e43a382e6ff6a9724f8dae137b93f5d5a61a3eb9d6e5213739b656c5d44

key type : ed25519

&#x20;

**Key Export All**

accumulate key export all export all keys in wallet

&#x20;

./accumulate key export all

private key : 470f9b6a34196895699ef3c40875ad3b05c6ad8486b74ee721f68288bd3ecb1c

public key : fe826e17daa861acad86539710bf08c709b1d9f88fe8e0d1d858912a4fe0b681

key type : unknown

&#x20;

**Key Export Private**

accumulate key export private \[key name] export the private key by key name

&#x20;

./accumulate key export private Key5

name : Key5

private key : c25288e8262fc23a5e8fc3acd523428b6913d05166f47022abef52acdba47930

public key : d5b57f10eb85a751094fcf943fc4997e45f0a90955294ca99cc5ee298d301690

key type : unknown

&#x20;

**Key Export Mnemonic**

accumulate key export mnemonic (export the mnemonic phrase if one was entered)

&#x20;

./accumulate key export mnemonic

mnemonic phrase: decide trap aisle raise above wool excite funny tuna body choice stereo

&#x20;

**Key Export Seed**

accumulate key export seed (export the seed generated from the mnemonic phrase)

&#x20;

./accumulate key export seed

seed: 2cca6f211913e1031f2acae938611e8599e24cd550f60c4ddb637fd28667aefd5eb7e1b04d366bd603678ae7a0b13452240efee6296a2c09e1460795f9796484

&#x20;

&#x20;

**Credits**

Credits are used to execute all Accumulate transactions, however actions done locally do not require credits such as constructing a key pair or constructing lite token account, lite identity account, or lite data account addresses. Only ACME tokens can be burned to generate Credits. Credits are nontransferable and do not fluctuate in value. Once credits are created, they cannot be converted back into ACME. Different transactions require more credits than others. All actions performed within an ADI need to reference a Key Page which holds credits for the ADI. A Sub-ADIs credit balance is dependent on its Key Pages and not the Parent ADIs Key Pages.

Estimated fees below are converted to USD.

&#x20;

| <p> </p><p>Type</p><p> </p>                                                                                                                                                                                     | <p> </p><p>Base Fee in Credits</p><p> </p> | <p> </p><p>Fee in USD approx.</p><p> </p> |
| --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------ | ----------------------------------------- |
| <p> </p><p>Construct a Lite Token Account Address</p><p> </p>                                                                                                                                                   | <p> </p><p>0</p><p> </p>                   | <p> </p><p>$0.00 </p><p> </p>             |
| <p> </p><p>Construct a Lite Identity Address</p><p> </p>                                                                                                                                                        | <p> </p><p>0</p><p> </p>                   | <p> </p><p>$0.00 </p><p> </p>             |
| <p> </p><p>Construct Lite Data Account Address</p><p> </p>                                                                                                                                                      | <p> </p><p>0</p><p> </p>                   | <p> </p><p>$0.00 </p><p> </p>             |
| <p> </p><p>Add Credits</p><p> </p>                                                                                                                                                                              | <p> </p><p>0</p><p> </p>                   | <p> </p><p>$0.00 </p><p> </p>             |
| <p> </p><p>Create Test ACME from Faucet</p><p> </p>                                                                                                                                                             | <p> </p><p>0</p><p> </p>                   | <p> </p><p>$0.00 </p><p> </p>             |
| <p> </p><p>Burn Tokens (Returns Tokens to Supply)</p><p> </p>                                                                                                                                                   | <p> </p><p>.1</p><p> </p>                  | <p> </p><p>$0.001 </p><p> </p>            |
| <p> </p><p>Create an Accumulate Digital Identity/Identifier (ADI)</p><p> </p>                                                                                                                                   | <p> </p><p>500</p><p> </p>                 | <p> </p><p>$5.00 </p><p> </p>             |
| <p> </p><p>Create an ADI Token Account</p><p> </p>                                                                                                                                                              | <p> </p><p>25</p><p> </p>                  | <p> </p><p>$0.25 </p><p> </p>             |
| <p> </p><p>Send Tokens</p><p> </p>                                                                                                                                                                              | <p> </p><p>3</p><p> </p>                   | <p> </p><p>$0.03 </p><p> </p>             |
| <p> </p><p>Create an ADI Data Account</p><p> </p>                                                                                                                                                               | <p> </p><p>25</p><p> </p>                  | <p> </p><p>$0.25 </p><p> </p>             |
| <p> </p><p>Create an ADI Scratch Data Account</p><p> </p>                                                                                                                                                       | <p> </p><p>25</p><p> </p>                  | <p> </p><p>$0.25 </p><p> </p>             |
| <p> </p><p>Write Data</p><p> </p>                                                                                                                                                                               | <p> </p><p>0.1</p><p> </p>                 | <p> </p><p>$0.001 </p><p> </p>            |
| <p> </p><p>Write Scratch Data</p><p> </p>                                                                                                                                                                       | <p> </p><p>0.01</p><p> </p>                | <p> </p><p>$0.0001 </p><p> </p>           |
| <p> </p><p>Create Token</p><p> </p>                                                                                                                                                                             | <p> </p><p>5000</p><p> </p>                | <p> </p><p>$50.00 </p><p> </p>            |
| <p> </p><p>Issue Token</p><p> </p>                                                                                                                                                                              | <p> </p><p>3</p><p> </p>                   | <p> </p><p>$0.03 </p><p> </p>             |
| <p> </p><p>Create Key Page</p><p> </p>                                                                                                                                                                          | <p> </p><p>100</p><p> </p>                 | <p> </p><p>$1.00 </p><p> </p>             |
| <p> </p><p>Create Key Book</p><p> </p>                                                                                                                                                                          | <p> </p><p>100</p><p> </p>                 | <p> </p><p>$1.00 </p><p> </p>             |
| <p> </p><p>Update Key Page</p><p> </p>                                                                                                                                                                          | <p> </p><p>3</p><p> </p>                   | <p> </p><p>$0.03 </p><p> </p>             |
| <p> </p><p>Update an Authority</p><p> </p>                                                                                                                                                                      | <p> </p><p>3</p><p> </p>                   | <p> </p><p>$0.03 </p><p> </p>             |
| <p> </p><p>Additional Signature</p><p> </p>                                                                                                                                                                     | <p> </p><p>0.1</p><p> </p>                 | <p> </p><p>$0.001 </p><p> </p>            |
|                                                                                                                                                                                                                 |                                            |                                           |
| <p> </p><p>All transactions incur a 0.1 credit fee per for each 256 bytes over a base 256 bytes.</p><p> </p>                                                                                                    |                                            |                                           |
| <p> </p><p>Failed transactions paying fees over 1 credit will be refunded less 1 credit. No refund is made for fees less than or equal to 1 credit.</p><p> </p>                                                 |                                            |                                           |
| <p> </p><p>Multi-sig will cost .001 for each additional signature</p><p> </p>                                                                                                                                   |                                            |                                           |
| <p> </p><p>First signer pays the transaction fee and each subsequent signer pays the signature fee</p><p> </p>                                                                                                  |                                            |                                           |
| <p> </p><p>All signatures incur a 0.1 credit fee per for each 256 bytes over a base 256 bytes.</p><p> </p><p>If adding credits fails, the ACME burned will be refunded less 1 credits worth of ACME</p><p> </p> |                                            |                                           |
| <p> </p><p>If a transaction fails at validation it gets thrown away and no credits are charged</p><p> </p>                                                                                                      |                                            |                                           |

&#x20;****&#x20;

&#x20;****&#x20;

**Adding Credits to a Lite Identity.**

accumulate credits \[origin token account] \[key page or lite identity url] \[number of credits wanted] \[max acme to spend] \[percent slippage (optional)] \[flags]\[BS2]&#x20;

&#x20;

To generate credits an ACME token account (Lite Token Account, ADI Token Account, Sub-ADI Token Account) must be referenced. By burning tokens, credits are created for your own accounts, or on behalf of another account. Because a Lite Token Account only has one public key, sharing the public key of the Lite Identity, a signing key does not have to be explicitly referenced in the transaction. The destination account for credits is either a Lite Identity or a Key Page. Key Pages will be explained in a following section. The number of credits wanted is self-explanatory. If price slippage occurs between the time the transaction is set up and executed, the maximum amount of ACME you are willing to spend can be stated. If the price increases the lower amount of ACME will be debited from the token account.

&#x20;

Credit Creation for a Lite Token Account/Lite Identity:

./accumulate credits acc://f338762f7013acb0fd5e1480c20df47ff836862adbd6e0f1/ACME acc://f338762f7013acb0fd5e1480c20df47ff836862adbd6e0f1/ACME  10000

&#x20;       Transaction Hash        : a743ab4412cc4ca8b08761e21d7bae7ddb2ed84e7e82a514a32e538eb5d79f08

&#x20;       Simple Hash             : 7e43cfcdb1acbc1f1f43d266013b2d48463fd2e5263f3cac3b89e4b08a52d9aa

&#x20;       Error code              : ok

&#x20;       Result                  : Oracle        $0.05 / ACME

&#x20;                                 Credits       10000.00

&#x20;                                 Amount        2000.00000000 ACME

&#x20;

&#x20;           **Use the TX History command to see prior transactions**

accumulate tx history \[url] \[starting transaction number] \[ending transaction number] Get transaction history

&#x20;

&#x20;           Trasaction History Start: 0      Count: 1        Total: 28

&#x20;

Receive 2000000.00000000 ACME to acc://f338762f7013acb0fd5e1480c20df47ff836862adbd6e0f1/ACME (cause: 6B93F1B7D9B43F0602027882777EC801C228CCED9CE489CE811984FC5635EFFD)

\---

&#x20; \- Transaction           : 1dbfc47eecf6d6c3a5b5b53f47495872a97278573f6e2acd822da626523eb90c

&#x20; \- Signer Url            : acc://f338762f7013acb0fd5e1480c20df47ff836862adbd6e0f1/ACME

&#x20; \- Signatures            :

&#x20;   \- Signer              : acc://bvn-BVN0/validators/1 (keyPage)

&#x20;     \-                   : synthetic

&#x20;     \-                   : ebb49298291fe0eaca71d863b8ecdfb308f19c5dee9b4536dbaa3b34c112dbbea52632a6c0cecc2193ef3cecb2be5be3eebe2a2ea5e86669111c51703752d10f (sig)

&#x20;     \-                   : 9b78185d5de99d4f0536d14034942e714a56a088e4e06cd920b9917fe0246bcb (key hash)

&#x20;     \-                   : receipt

&#x20; \- Signatures            :

&#x20;   \- Signer              : acc://dn/validators/1 (unknownSigner)

&#x20;     \-                   : receipt

&#x20;****&#x20;

**Oracle**

To explicitly query the oracle to see the current price of ACME and number of credits per ACME:

./accumulate oracle

&#x20;****&#x20;

**USD per ACME : $0.0500**

**Credits per ACME : 5.00**

&#x20;

**Lite Data Accounts**

Lite Data Accounts are an extension of the Factom Protocol, which will be used to transition data from Factom to Accumulate. Lite Data Accounts have no direct relation to Lite Identities or Lite Token Accounts. In the same manner as a Lite Token account, you can construct a Lite data account address without creating the account. For the protocol to know of a Lite Data Accounts existence, data must be written to it. This can either be at the time of creation of the Lite Data Account or afterwards.  **** &#x20;

&#x20;****&#x20;

**Lite Data Account Creation from Lite Toke Account/Lite Identity**

account create data --lite \[lite token account URL] \[data (chain name)]

./accumulate account create data --lite acc://f338762f7013acb0fd5e1480c20df47ff836862adbd6e0f1/ACME "Ben"                       &#x20;

&#x20;       Account Url             :acc://c26fd6ed6beafd197086c420bbc334f0cd4f05802b550e5d

&#x20;

&#x20;       Account Id              :c26fd6ed6beafd197086c420bbc334f0cd4f0580a44dc689452b57b150d10e46

&#x20;       Entry Hash              :cda19cfa7cc15bcf1ce2dea451c13a0f8a77e15fee6289c0839f4f176d357bce

&#x20;       Transaction Hash        : 62f4c555e8d95b00a775337c54cac80ab6222d6bdf7c4f8eadc013830b9b1fc4

&#x20;       Signature 0 Hash        : 89bfdd4619147eb32590cb83f8d05d73697f6f8a31a6961df3e0a8feaaa41b1e

&#x20;       Simple Hash             : 05ea5c5b406964af4f4a5adc52d5c8ef6e5565ec9de21415847310e5e5980a40

&#x20;       Error code              : ok

&#x20;       Result                  :

&#x20;

**Lite Data Account Creation from ADI**

Account create data  --lite \[origin token account]\[signing key]\[extID]

./accumulate account create data --lite acc://DefiDevs.acme Key2 "Marian"\
\


&#x20;       Account Url             :acc://7d27485702b1f756a7c0f6ac39931e77959f58d475ee3898

&#x20;

&#x20;       Account Id              :7d27485702b1f756a7c0f6ac39931e77959f58d4598949d4fd9dfd8f98358c04

&#x20;       Entry Hash              :071b9662b4c3512d4c0b3dbdd73fc092e155abe805aad3ec14a1183fb732b960

&#x20;       Transaction Hash        : eac6868a7e756faca5e00e999efadec6967eab5c9b7b434b4c6160bda6e7a283

&#x20;       Signature 0 Hash        : 31c2b9d9e9457dc484a3dc2260b20bc6d34f2876196fabc531279c6100145a1f

&#x20;       Simple Hash             : d28c28d27ec764bcf3218c10abcdf69e23024461c102331e35cd221c0663580a

&#x20;       Error code              : ok

&#x20;       Result                  :

&#x20;

**Writing to a Lite Data Account**

accumulate data write-to \[account url] \[signing key]\[BS3]  \[lite data account] \[extid\_0 (optional)] ... \[extid\_n (optional)] \[data]

&#x20;

data write-to acc://0143b52490530b90eef9b1a2405e322c6badc1e90e200c56/ACME acc://7d27485702b1f756a7c0f6ac39931e77959f58d475ee3898 "Key6"

&#x20;

&#x20;       Account Url             :acc://7d27485702b1f756a7c0f6ac39931e77959f58d475ee3898

&#x20;

&#x20;       Account Id              :7d27485702b1f756a7c0f6ac39931e77959f58d4598949d4fd9dfd8f98358c04

&#x20;       Entry Hash              :185f8db32271fe25f561a6fc938b2e264306ec304eda518007d1764826381969

&#x20;       Transaction Hash        : f27277b07e66883c836a72020d50e57cc8c1e86f24307ac99e2a4c035f6f8973

&#x20;       Signature 0 Hash        : 0b4fbe4878374e5dd7aafb10dbe23f141998dd3603ee35dd930102f80cc256cf

&#x20;       Simple Hash             : e8b203831aa0de000a9e26e60c44d8167c272d2e53dcb99c0785dfd7bd6ede15

&#x20;       Error code              : ok

&#x20;       Result                  :

&#x20;

**Querying a Lite Data Account by URL**

accumulate data get \[DataAccountURL]                    Get most current data entry by URL

./accumulate data get acc://7d27485702b1f756a7c0f6ac39931e77959f58d475ee3898

{"type":"dataEntry","mainChain":{"height":2,"count":2,"roots":\["04b097c244655110e76f77dfeaf39910af96d4c651037c05cdc841872f53d11a","8e70b62e509e6f037b69f205a8355c0586ce7e26457411d781dfe8de0eecedc7"]},"data":{"entry":{"data":\["48656c6c6f"]},"entryHash":"f522210a71e681a1f7f40d005322dc36fb6bcbe915889dd9f1aa78147703ee38"},"chainId":"a2bd8fbd9b14eef22f157079cb3a99067d87fd3b9923e423fdf051e55d116a01"}

&#x20;

**Querying a Lite Data Account by URL and a Specific Entry Hash**

accumulate data get \[DataAccountURL] \[EntryHash]  Get data entry by entryHash in hex

./accumulate data get acc://7d27485702b1f756a7c0f6ac39931e77959f58d475ee3898 071b9662b4c3512d4c0b3dbdd73fc092e155abe805aad3ec14a1183fb732b960

{"type":"dataEntry","mainChain":{"height":2,"count":2,"roots":\["04b097c244655110e76f77dfeaf39910af96d4c651037c05cdc841872f53d11a","8e70b62e509e6f037b69f205a8355c0586ce7e26457411d781dfe8de0eecedc7"]},"data":{"entry":{"data":\["","4d617269616e"]},"entryHash":"071b9662b4c3512d4c0b3dbdd73fc092e155abe805aad3ec14a1183fb732b960"},"chainId":"a2bd8fbd9b14eef22f157079cb3a99067d87fd3b9923e423fdf051e55d116a01"}

&#x20;

**Querying a Lite Data Account by URL and Index**

&#x20; accumulate data get \[DataAccountURL] \[start index] \[count] expand(optional) Get a set of data entries starting from start and going to start+count, if "expand" is specified, data entries will also be provided

./accumulate data get acc://7d27485702b1f756a7c0f6ac39931e77959f58d475ee3898 0 2                 &#x20;

{"type":"dataSet","items":\[{"entry":{},"entryHash":"071b9662b4c3512d4c0b3dbdd73fc092e155abe805aad3ec14a1183fb732b960"},{"entry":{},"entryHash":"f522210a71e681a1f7f40d005322dc36fb6bcbe915889dd9f1aa78147703ee38"}],"start":0,"count":2,"total":2}

&#x20;****&#x20;

&#x20;****&#x20;

&#x20;****&#x20;

**Accumulate Digital Identity/Identifier (ADI)**

The atomic unit of Accumulate is an ADI. An ADI is a human readable URL which holds different account types, such as ana . An ADI holds Key Books which contain prioritized Key Pages. ADI names are unique and once created cannot be generated by a different party.\
\


Example ADI:

Acc://{Identity name}/{key book name}/1

The name of the identity is chosen by a user. Identities are unique. A user can also name their Key Book. The Key Page defaults to 1 when creating an ADI. Each successive Key Page is n + 1 of the prior Key Page.

&#x20;

**ADI Creation:**

When creating an Identity, you specify a human readable URL. Like the creation of any Account, the creation of an ADI requires a token account to be referenced for the burning of ACME to mint credits. The public key of the Lite Token Account/Lite Identity can be referenced or the public key or key name of different key. Key Books contain Key Pages which has entries that define the set of Public Key Hashes or Key Book URLs required to validate a transaction. During ADI Creation a Key Book name can be specified while a Key Page defaults to 1. ADI’s can be created from any ADI account type that has credits.

&#x20;****&#x20;

**ADI Creation from a Lite Token Account:**

accumulate adi create \[origin-lite-account] \[adi url to create] \[public-key or key name] \[key-book-name (optional)] \[public key page 1 (optional)]  Create new ADI from lite token account.

When public key 1 is specified, it will be assigned to the first page, otherwise the origin key is used.

A key was generated called Key1 which will be assigned to the first Key Page.

./accumulate adi create acc://f338762f7013acb0fd5e1480c20df47ff836862adbd6e0f1/ACME  acc://DefiDevs.acme Key1 acc://DefiDevs.acme/Keybook

&#x20;

&#x20;       Transaction Hash        : 1139db355819257a618129641464b145e8a4d0fdab301507f7c0ebbcd9185105

&#x20;       Signature 0 Hash        : cf3dbe8c63b9f31b5a506de03cf758393e1db6c71e039b7c528d7651b9128b8c

&#x20;       Simple Hash             : a08ab66047f800ce11e0654bae6b584d085fd594c70c225a3aa87cbd9e0bc597

&#x20;       Error code              : ok

&#x20;       Result                  :

&#x20;

**ADI Creation from an ADI:**

accumulate adi create \[origin-adi-url] \[wallet signing key name] \[key index (optional)] \[key height (optional)] \[adi url to create] \[public key or wallet key name] \[key book url (optional)] \[public key page 1 (optional)] Create new ADI for another ADI

./accumulate adi create acc://DefiDevs.acme Key2 acc://Toyota Key2 acc://Toyota/Keybook

&#x20;

&#x20;       Transaction Hash        : 00038a5fd818006ac01089f8aea782b846722bec150a333dfc77356a277e60bf

&#x20;       Signature 0 Hash        : 5c64193d64950c2bee4873feb557d477ca0590fd37e4b0b4ad817a5fdd1fcdb4

&#x20;       Simple Hash             : 032d354fc6b03036f00cb5cfdf2674705a2e5f0f2f99896b9ceea48e77feaad9

&#x20;       Error code              : ok

&#x20;       Result                  :

&#x20;

_**ADIs can also be created by Creation from an ADI Data Account, ADI Token Account, ADI Token Issuance as well as a Sub-ADI and its Accounts.**_

&#x20;

**ADI Creation from a Sub-ADI:**

accumulate adi create \[origin-adi-url] \[wallet signing key name] \[key index (optional)] \[key height (optional)] \[adi url to create] \[public key or wallet key name] \[key book url (optional)] \[public key page 1 (optional)] Create new ADI for another ADI

./accumulate adi create acc://DefiDevs.acme/Robot Key2 acc://Ford Key2 acc://Ford/Keybook

&#x20;

&#x20;       Transaction Hash        : e3fa9f05a4eb736dbaac58594fdcfb1478098555d7c27c315a4595a38aabdd5e

&#x20;       Signature 0 Hash        : c00282900903ddf18f7ca2fcbe09bd2971d48d8364516e45d9f7069ecb1db7b7

&#x20;       Simple Hash             : 23c66ccbe1bba178b553c87582595d2710e7e97d85528c96c37d5ae07ebfebe3

&#x20;       Error code              : ok

&#x20;       Result                  :

&#x20;****&#x20;

**ADI Creation from a Sub-Sub-ADI**

accumulate adi create \[origin-adi-url] \[wallet signing key name] \[key index (optional)] \[key height (optional)] \[adi url to create] \[public key or wallet key name] \[key book url (optional)] \[public key page 1 (optional)] Create new ADI for another ADI

&#x20;

./accumulate adi create acc://DefiDevs.acme/Robot/MrRoboto Key2 acc://Ferrari Key2 acc://Ferrari/Keybook

&#x20;

&#x20;       Transaction Hash        : a203c790287deb440c2fb1abeaab92131ea0ce4deaeb1d2c448bf2ba92b9dac6

&#x20;       Signature 0 Hash        : e095e22c1e20d89f0b741332200d647febc86369826f3c65000e842f99cbef35

&#x20;       Simple Hash             : f4509afb159a11ece81f89395f512e9f0bf40b16c0a007140b8606dd6ba23f93

&#x20;       Error code              : ok

&#x20;       Result                  :

&#x20;****&#x20;

**ADI Directory**

To see the accounts within a specific ADI:

&#x20;

accumulate adi directory \[url] \[from] \[to] \[flags]

&#x20;

./accumulate adi directory acc://DefiDevs.acme 0 20

&#x20;

&#x20;       ADI Entries: start = 0, count = 20, total = 11

&#x20;       acc://DefiDevs.acme/Keybook (Key Book)

&#x20;       acc://DefiDevs.acme/Tokens (ADI Token Account)

&#x20;       acc://DefiDevs.acme/Data (Data Chain)

&#x20;       acc://DefiDevs.acme/ScratchData (Data Chain)

&#x20;       acc://DefiDevs.acme/Keybook2 (Key Book)

&#x20;       acc://DefiDevs.acme/Car (ADI)

&#x20;       acc://DefiDevs.acme/Robot (Sub-ADI)

&#x20;       acc://DefiDevs.acme/Cybertruck (Sub-ADI)

&#x20;       acc://DefiDevs.acme/AI (tokenIssuer)

&#x20;       acc://DefiDevs.acme/AITokens (ADI Token Account)

&#x20;****&#x20;

**ADI List**

To see a list of ADIs created and the initial Key specified for Key Page 1 (explained in a future section)

acc://GM        :       Key3

acc://Google    :       Key1

acc://DefiDevs.acme     :       Key2

&#x20;

**ADI Get**

ADI get returns the ADI URL as well as the Key Book generated during the creation of the ADI.

&#x20;

accumulate adi get \[url] \[flags]

./accumulate adi get acc://DefiDevs.acme

&#x20;

&#x20;       ADI url         :       acc://DefiDevs.acme

&#x20;       Key Book Url    :       acc://DefiDevs.acme/Keybook

&#x20;****&#x20;

**Key Books**

Key Books store the Hierarchical Key Management Structure of an ADI using Key Pages and Keys within those pages. A Key Book is an ordered set of Key Pages by priority where any Key Page can modify itself or a Page of lower priority unless the Key Page is locked. Modifications include adding, updating, or removing keys. An ADI can have multiple Key Books. An Account specifies what Key Book(s) it will use for transactions. Key Books are assigned to accounts such as ADI Token Accounts and ADI Data Accounts, whereby the Key Book determines which Key Page and Keys it wants to use to execute transactions for ADI Token Accounts and ADI Data Account.

For the ADI Created above, a get command on the Key Book can be performed which shows the index of the Key Book as well as the public key and key name. Unless otherwise specified, Key Books don’t have a relationships to one another.

&#x20;

accumulate get \[url]          Get data by Accumulate URL

&#x20;

**Get Key Book**

&#x20;

./accumulate get acc://DefiDevs.acme/Keybook/

&#x20;

Page Count

&#x20;       2

get         Deprecated - use \`accumulate get ...\` fix in CLI

&#x20;

**Create an Additional Key Book**

An ADI can have multiple Key Books. To create an additional Key Book, a Public Key Hash or Key Book URL must be specified for the purpose of signing the transaction. A new public key or specified public key name should be added to the new book.

&#x20;

&#x20; accumulate book create \[origin adi url] \[signing key name] \[key index (optional)] \[key height (optional)] \[new key book url] \[public key 1 (optional)] ... \[public key hex or name n + 1 \[flags]

./accumulate book create acc://DefiDevs.acme Key1 acc://DefiDevs.acme/Keybook2 Key3

&#x20;

&#x20;       Transaction Hash        : c168ecfb3985a88f694666b0ed19f8e24b6451eb412da788f1068694a24e4a24

&#x20;       Signature 0 Hash        : 0c023834a44520f396470c0db58404db94330aee7189a78073463d017d2736a1

&#x20;       Simple Hash             : 48f0c4a86d6c1d45e8de4d718370aa6481da9f09c853f53135b5858de85d976c

&#x20;       Error code              : ok

&#x20;       Result                  :

&#x20;

**Key Pages**

A Key Page has entries that defines what parties are required to validate a transaction. An entry can contain and Public Key Hash, Key Book URL, or a Public Key Hash and Key Book URL. For a Key Book URL to be added to the Key Page the Owner of the Key Book must sign a transaction to authorize it. Key Pages have an m of n, m representing the signature threshold and n representing the total number of signators. In addition, Key Pages have voting rules. By default, a Key Page’s m of n is an acceptance threshold. In future releases a rejection threshold can be added as well as the ability to abstain from voting. Key Pages are ordered by priority where any Key Page can modify itself or a Page of lower priority unless the Key Page is locked. Key Pages store credits for all the Accounts that are defined within the ADI. A Key Page for the signing Key does not have to be explicitly specified if the name of the signing key is unique. If two Key Pages have the same signing key name, then the page must be specified in the transaction. There must always be one Key in the highest priority Key Page.

&#x20;

For the ADI Created above, a get command on the Key Page can be performed which shows the index of the of the Key within the Key Page as well as the public key and key name.

&#x20;

**Get Key Page**

&#x20;

accumulate get \[url]          Get data by Accumulate URL

&#x20;

./accumulate get acc://DefiDevs.acme/Keybook/1

&#x20;

&#x20;       Index   Nonce           Public Key                                                              Key Name(s)

&#x20;       0       1969-12-31 19:00:00 -0500 EST           272b7a64c2caf76ffe6cf0adf37a144aff60920bdc269803982f150802053afb                             Key1

&#x20;

**Adding Credits to a Key Page**

An ACME token account must be referenced when adding credits to a Key Page. This can either be a Lite Token Account or an ADI Token Account which will be explained in a future section.

&#x20;

accumulate credits \[origin token account] \[key page or lite identity url] \[number of credits wanted] \[max acme to spend] \[percent slippage (optional)] \[flags]

&#x20;

**Add Credits to Key Page**

./accumulate credits acc://f338762f7013acb0fd5e1480c20df47ff836862adbd6e0f1/ACME acc://DefiDevs.acme/Keybook/1 10000

&#x20;

&#x20;       Transaction Hash        : 7bba5f1178d71193a91641ad627d8d232b88f4f0a37cb855bef5afa1b741aa1a

&#x20;       Simple Hash             : 00da35f2201a5a6143375d9225188ac49f1129c7c748bd7f6c0f2d218eb85b2a

&#x20;       Result                  : Oracle        $0.05 / ACME

&#x20;                                 Credits       10000.00

&#x20;                                 Amount        2000.00000000 ACME

&#x20;

**Adding Additional Key Pages to a Key Book**

A new Key Page can be added to a Key Book where public keys or key names can be specified. In the example below 3 keys were added to the new Key Page (Key1, Key3, and Key4. Due to this being the 2nd Key Page, the Key Page URL would be acc:/DefiDevs.acme/Keybook/2.

./accumulate page create acc://DefiDevs.acme/Keybook Key1 Key3 Key4

&#x20;

&#x20;       Signature 0 Hash        : dee40ebb838385eb43c78edd325cf4ad1c54c4e68dd73e8b4454348aea8a849b

&#x20;       Simple Hash             : cb61cd5f34b2785da2763ac8ca773c2c19a60410f734bb7cb230fd8bc4fc009f

&#x20;       Error code              : ok

&#x20;       Result                  :

&#x20;

**Get Key Page**

To see the Key Names and Public Keys within the Key Page the Page Get command will query the Key Page

&#x20;

accumulate page get \[url] \[flags]

&#x20;

./accumulate page get  acc://DefiDevs.acme/Keybook/2

&#x20;

&#x20;       Credit Balance  :       0.00

&#x20;

&#x20;       Index   Nonce           Public Key                                                              Key Name(s)

&#x20;       0       1969-12-31 19:00:00 -0500 EST           fa9ae1e76b6936583546d495c98f34a9f0d57b52f759b4ebf1f04e6db0111381                             Key3

&#x20;       1       1969-12-31 19:00:00 -0500 EST           c3781e20dd3dbaade511587e4b153efc86e2194111a07091a0e6159d7699c513                             Key4

&#x20;       2       1969-12-31 19:00:00 -0500 EST           0d83eababd1ba323f69470576f8c9eb563821a07cca55f5ac30f276cf62bebc4                             Key1

&#x20;****&#x20;

**Adding, Updating, or Removing a Key **_**within the same Key Page**_

Within a Key Page, a Key can be added, updated, or removed. In the example below a new Key named Key2 is being added to Key Page 1 of the DefiDevs.acme ADI’s Key Book. Regardless of the m of n of a Key Page the owner of the Key can always add, update, or remove their own Key.

&#x20;

**Adding a Key**

accumulate page key add \[key page url] \[signing key name] \[key index (optional)] \[key height (optional)] \[new key name] \[flags]

&#x20;

./accumulate page key add acc://DefiDevs.acme/Keybook/1 Key1 Key2

Transaction Hash        : 9fbcbe49b4dbbf861be63eeae41576f1da7b7ca3b31e1c3968adff766b0445c2

Signature 0 Hash        : 99f87aa951585592d66a56e670b083c8a4f10de0fd014a72b2d05fa901546dde

Simple Hash             : f4f7e5e0d8b5599aad214412939f954b4bf012b8f5ac9a56d24d54983f185d3d

&#x20;            Error code              : ok

&#x20;            Result                  :

&#x20;

**Query Page**

A get command will query the Key Page to show the new key that has been added.

&#x20;

accumulate get \[url]          Get data by Accumulate URL

&#x20;

./accumulate get acc://DefiDevs.acme/Keybook/1

&#x20;

&#x20;       Credit Balance  :       9997.00

&#x20;

&#x20;       Index   Nonce           Public Key                                                              Key Name(s)

&#x20;       0       1969-12-31 19:00:00 -0500 EST           272b7a64c2caf76ffe6cf0adf37a144aff60920bdc269803982f150802053afb        Key1

&#x20;       1       1969-12-31 19:00:00 -0500 EST           f619aa889a2532d2d331d8a1287895b87605d7a5a1c75ad671f9bb6a7628940c        Key2

&#x20;

**Removing a Key**

accumulate page key remove \[key page url] \[signing key name] \[key index (optional)] \[key height (optional)] \[old key name] \[flags]

&#x20;

./accumulate page key remove acc://DefiDevs.acme/Keybook/1 Key2 Key2

&#x20;

&#x20;       Transaction Hash        : c237853496f3348e8dd9fc847bb692608a1d9ed95236d351908203691951b749

&#x20;       Signature 0 Hash        : ecb1aa735f8473d8d0b0194549d9ec94be520b1ee6c24e4846b0b7b122ebf932

&#x20;       Simple Hash             : 5355696f77cfc89d0f5b3be90dccb66e7f337af303d2c66129de8c8ba5b02aed

&#x20;       Error code              : ok

&#x20;       Result                  :

&#x20;

**Query Page**

A get command will query the Key Page to show that the new key has been removed.

&#x20;

accumulate get \[url]          Get data by Accumulate URL

&#x20;

./accumulate get acc://DefiDevs.acme/Keybook/1                                  &#x20;

&#x20;

&#x20;       Credit Balance  :       9994.00

&#x20;

&#x20;       Index   Nonce           Public Key                                                              Key Name(s)

&#x20;       0       1969-12-31 19:00:00 -0500 EST           272b7a64c2caf76ffe6cf0adf37a144aff60920bdc269803982f150802053afb        Key1

&#x20;

**Updating a Key**

accumulate page key update \[key page url] \[signing key name] \[key index (optional)] \[key height (optional)] \[old key name] \[new public key or name] \[flags]

&#x20;

./accumulate page key update acc://DefiDevs.acme/Keybook/1 Key1 Key1 Key2

&#x20;

**Query Page**

&#x20;****&#x20;

A get command will query the Key Page to show that a key has been updated.

&#x20;

accumulate get \[url]          Get data by Accumulate URL

&#x20;

./accumulate get acc://DefiDevs.acme/Keybook/1

&#x20;

&#x20;       Credit Balance  :       9991.00

&#x20;

&#x20;       Index   Nonce           Public Key                                                              Key Name(s)

&#x20;       0       1969-12-31 19:00:00 -0500 EST           f619aa889a2532d2d331d8a1287895b87605d7a5a1c75ad671f9bb6a7628940c        Key2

&#x20;

**Adding, Updating, or Removing a Key **_**of a Lower Priority Key Page**_

The ADI acc://DefiDevs.acme has two Key Pages. The Key Page of the highest priority acc://DefiDevs.acme/Keybook/1 (1 being the highest priority) can modify itself and add, update, or remove Keys or a Key Book URL of a lower priority Key Page such as acc://DefiDevs.acme/Keybook/2. A Key Page of a lower priority cannot modify a Key Page of a higher priority. A get command of both Key Pages will show the current set of Keys on those pages.

&#x20;

**Query Key Page 1**

&#x20;

accumulate get \[url]          Get data by Accumulate URL

&#x20;

./accumulate get acc://DefiDevs.acme/Keybook/1

&#x20;

&#x20;            Credit Balance  :       9991.00

&#x20;

&#x20;            Index   Nonce           Public Key                                                              Key Name(s)

&#x20;            0       1969-12-31 19:00:00 -0500 EST           f619aa889a2532d2d331d8a1287895b87605d7a5a1c75ad671f9bb6a7628940c        Key2

&#x20;

The only Key in Key Page 1 is Key2

&#x20;

**Query Key Page 2**

./accumulate get acc://DefiDevs.acme/Keybook/2

&#x20;

&#x20;    Credit Balance  :       10000.00

&#x20;

&#x20;       Index   Nonce           Public Key                                                              Key Name(s)

&#x20;       0       2022-05-10 21:51:26.344157 -0400 EDT            fa9ae1e76b6936583546d495c98f34a9f0d57b52f759b4ebf1f04e6db0111381        Key3

1       1969-12-31 19:00:00 -0500 EST           c3781e20dd3dbaade511587e4b153efc86e2194111a07091a0e6159d7699c513        Key4

2       1969-12-31 19:00:00 -0500 EST           0d83eababd1ba323f69470576f8c9eb563821a07cca55f5ac30f276cf62bebc4        Key5

&#x20;

In the following examples the Key in Key Page 1 will be used to modify the Keys of Key Page 2 which is a lower priority Key Page:

&#x20;

**Adding a Key to a Lower Priority Page using a Higher Priority Key Page**

The Key Page URL will be that of the Key Page you are adding the Key to. In this instance it is Key Page 2. The signing Key will be from Key Page 1.

accumulate page key add \[key page url] \[signing key name] \[key index (optional)] \[key height (optional)] \[new key name] \[flags]

&#x20;

./accumulate page key add acc://DefiDevs.acme/Keybook/2 Key2 Key6

&#x20;

&#x20;       Transaction Hash        : b9dfe4ae58915aea200444843665a8606916b0187ba8e9615c3f11e333e216bf

&#x20;       Signature 0 Hash        : 2651e478946fb6a42154e7a670cb39adc041263e458c14c6737ef791352f50eb

&#x20;       Simple Hash             : 1c47ff6705f03588eb35efeb04aa8733d24c30ab5ff434dbd579c442bb3e32b5

&#x20;       Error code              : ok

&#x20;       Result                  :

&#x20;

**Query Key Page 2**

./accumulate get acc://DefiDevs.acme/Keybook/2

&#x20;

&#x20;       Credit Balance  :       10000.00

&#x20;

&#x20;       Index   Nonce           Public Key                                                              Key Name(s)

&#x20;       0       1969-12-31 19:00:00 -0500 EST           fa9ae1e76b6936583546d495c98f34a9f0d57b52f759b4ebf1f04e6db0111381        Key3

1       1969-12-31 19:00:00 -0500 EST           c3781e20dd3dbaade511587e4b153efc86e2194111a07091a0e6159d7699c513        Key4

2       1969-12-31 19:00:00 -0500 EST           0d83eababd1ba323f69470576f8c9eb563821a07cca55f5ac30f276cf62bebc4        Key5

3       1969-12-31 19:00:00 -0500 EST           2ca7b29ce5da412df4b2e8ff391ffe17f2a4014b250e94526849391f67f38328        Key6

&#x20;

**Removing a Key of a Lower Priority Key Page using a Higher Priority Key Page**

accumulate page key remove \[key page url] \[signing key name] \[key index (optional)] \[key height (optional)] \[old key name] \[flags]

&#x20;

./accumulate page key remove acc://DefiDevs.acme/Keybook/2 Key2 Key4

&#x20;****&#x20;

&#x20;       Transaction Hash        : f5b4ab98ff3b322bf513376acaad748d65847408c6b3e10909e32bd1c81401d9

&#x20;       Signature 0 Hash        : d9e3c4786353b89d1fa7bca22e2e317f2e4071e195e86f6f2bfd409d0516cb63

&#x20;       Simple Hash             : ffe7d185949a7322333a485590c8976fc1dd66855f7fc973dfae084f1afb455a

&#x20;       Error code              : ok

&#x20;       Result                  :

&#x20;

&#x20;           **Query Key Page 2**

./accumulate get acc://DefiDevs.acme/Keybook/2 -s https://testnet2.accumulatenetwork.io/v2                                   &#x20;

&#x20;

&#x20;       Credit Balance  :       10000.00

&#x20;

&#x20;       Index   Nonce           Public Key                                                              Key Name(s)

0         1969-12-31 19:00:00 -0500 EST         &#x20;

fa9ae1e76b6936583546d495c98f34a9f0d57b52f759b4ebf1f04e6db0111381        Key3

1         1969-12-31 19:00:00 -0500 EST         &#x20;

0d83eababd1ba323f69470576f8c9eb563821a07cca55f5ac30f276cf62bebc4        Key5

2         1969-12-31 19:00:00 -0500 EST         &#x20;

2ca7b29ce5da412df4b2e8ff391ffe17f2a4014b250e94526849391f67f38328        Key6

&#x20;

**Updating a Key of a Lower Priority Key Page using a Higher Priority Key Page**

accumulate page key update \[key page url] \[signing key name] \[key index (optional)] \[key height (optional)] \[old key name] \[new public key or name] \[flags]

&#x20;

./accumulate page key update acc://DefiDevs.acme/Keybook/2 Key2 Key6 Key7

&#x20;

&#x20;       Transaction Hash        : 9650efb1ba0a56ae2f148b4f94a5d1eb0a91da18f669de5a5df4346212d602b8  &#x20;

&#x20;       Signature 0 Hash        : caace5fbd0e256d19fb2907b2db632a28fffec135f1781697d8299736f0bdcf6  &#x20;

&#x20;       Simple Hash             : d72cb8eac4dd8d497653628791970aa9a4bdeb79cfbbc296ed244107986212b9  &#x20;

&#x20;       Error code              : ok

&#x20;       Result                  :

&#x20;

**Query Key Page 2**

./accumulate get acc://DefiDevs.acme/Keybook/2

&#x20;

&#x20;       Credit Balance  :       10000.00

&#x20;

&#x20;       Index   Nonce           Public Key

&#x20; Key Name(s)

&#x20;       0       1969-12-31 19:00:00 -0500 EST           fa9ae1e76b6936583546d495c98f34a9f0d57b52f759b4ebf1f04e6db0111381      Key3

&#x20;       1       1969-12-31 19:00:00 -0500 EST           0d83eababd1ba323f69470576f8c9eb563821a07cca55f5ac30f276cf62bebc4      Key5

&#x20;       2       1969-12-31 19:00:00 -0500 EST           973bb47d1073799fd9600b2c5e24439e9cfbac437f4dac1f0313788b13a276f1      Key7

&#x20;

**Locking and Unlocking Key Pages of Lower Priorities**

Add the ability to lock a key page. A locked key page cannot modify (or add) keys. A locked key page cannot execute ‘UpdateKeyPage’ except when a key is modifying its own spec (keys can still update themselves). A locked key page also cannot execute ‘CreateKeyPage’ or ‘CreateKeyBook.’

&#x20;

**Lock a Key Page**

accumulate page lock \[key page url] \[signing key name] \[key index (optional)] \[key height (optional)] \[flags]

&#x20;

./accumulate page lock acc://DefiDevs.acme/Keybook/2 Key2

&#x20;

&#x20;       Transaction Hash        : 77c2ee9bac6e5be34d236584f885a58fb68f89f66007544635a2d2397875a050

&#x20;       Signature 0 Hash        : fb9d9fdbd9db138bcce5129f2bcfed95c2f9432fcf851085a432c2ab05b9a8ef

&#x20;       Simple Hash             : 1e3f97308e583d8462ffa7c14eab774587b0f7cf0745c303e540f03ba80bf322

&#x20;       Error code              : ok

&#x20;       Result                  :

&#x20;

**Unlock a Key Page**

accumulate page unlock \[key page url] \[signing key name] \[key index (optional)] \[key height (optional)] \[flags]

./accumulate page unlock acc://DefiDevs.acme/Keybook/2 Key2

&#x20;

&#x20;       Transaction Hash        : 95e7c4788e84b4f5352ce8469617a6dc2ae896426190e022b4ec111f1ff28051

&#x20;       Signature 0 Hash        : c89b3129ce2b347807f6d627ca4e48a2da5a3862f34712ff3b7d248a4e790a58

&#x20;       Simple Hash             : 12c149fd4674a12e8ca181b40c9837c140e6bd13640c08712880913deea11736

&#x20;       Error code              : ok

&#x20;       Result                  :

&#x20;****&#x20;

&#x20;****&#x20;

**Setting a Threshold for a Key Page**

By default, when setting a threshold for a Key Page the m of n will be 1 of 1. Because of this, any entry within the Key Page can update the signature threshold. In the example below, the number of Keys within acc://DefiDevs.acme/Keybook/2 is 3. Setting the threshold at 2, means that 2 of 3 signatures are required for the transaction to be processed.

&#x20;

./accumulate tx execute acc://DefiDevs.acme/Keybook/2 Key1 '{\\"type\\": \\"updateKeyPage\\", \\"operation\\": \[{ \\"type\\": \\"setThreshold\\", \\"threshold\\": 2 }]}'

&#x20;

&#x20;       Transaction Hash        : 6130d09c7b8bc2ffbdf82f13b9a0a4b5144bc2878523e899549ed732c9829f22

&#x20;       Signature 0 Hash        : 2990a1ee1894494859162ed9d6772454a55a8737960fcaa09e7f6d150c8ef944

&#x20;       Simple Hash             : 881275aea93bd90879f8f8d6c4d7d479ccffdc18b31f89538c752f67b77b0368

&#x20;       Error code              : ok

&#x20;       Result                  :

&#x20;

**Multi-Signature Transactions**

A multi-signature transaction is defined by the signature threshold for a given Key Page. In the following examples, a new Key will be added to a Key Page using a multi-signature transaction.

&#x20;

./accumulate page key add acc://DefiDevs.acme/Keybook/2 Key5 Key1

&#x20;

&#x20;       Transaction Hash        : 72fb5fcdecbf8b30182e20eaeb4d218f13163fe15b2ff6543f8be7ea2d4a78e6

&#x20;       Signature 0 Hash        : de3f985a3569b3537c591353db6a15a385578967b7ddc28910f6779bebce4cf3

&#x20;       Simple Hash             : 8961c92b3adeadaae13eba36e935808d723c33806bc421937159d0a9498b33c6

&#x20;       Error code              : ok

&#x20;       Result                  :

&#x20;

A pending transaction can be queried to see the status.

**./accumulate tx pending 72fb5fcdecbf8b30182e20eaeb4d218f13163fe15b2ff6543f8be7ea2d4a78e6**

&#x20;       **Pending Tranactions -> Start: 0  Count: 1       Total: 1**

&#x20;

The second signer signs the transaction hash of the first transaction in the multi-signature sequence. If there are additional signers, they sign the same transaction hash.

&#x20;

./accumulate tx sign acc://DefiDevs.acme/Keybook/2 Key3 72fb5fcdecbf8b30182e20eaeb4d218f13163fe15b2ff6543f8be7ea2d4a78e6     &#x20;

&#x20;

&#x20;       Transaction Hash        : 72fb5fcdecbf8b30182e20eaeb4d218f13163fe15b2ff6543f8be7ea2d4a78e6

&#x20;       Signature 0 Hash        : de79633b1ceced2652f29f7fcb813190c19d175dd1846e76b3e233da66252666

&#x20;       Simple Hash             : c87ef41af1233a666e9a833f50ee030ddcca08a1adaab76904846489220f3b8b

&#x20;       Error code              : ok

&#x20;       Result                  :

&#x20;

**Transaction Signing Schemes and Delegators, and Delegates**

How a Key Book signs a transaction is dependent on the rules of the Key Page. There are three options for how an entry within a Key Page can be represented.

1\.     Public Key Hash

The Public Key hash is presumably a Key that is generated locally or remotely that will be used to sign a transaction.

2\.     Public Key Hash and Delegate (Key Book URL)\*

If an entry specifies both a Public Key Hash and a Key Book URL, either can sign a transaction

If a Key Book URL is used the Key Book is a Delegate, because the signing power and how the transactions are signed is up to the Key Book owner.

When adding a Key Book to a Key Page, the owner of the Key Book URL must sign a transaction to approve the addition of their Key Book to the Key Page.

3\.     Delegate\*

If an entry specifies a Key Book URL, the Key Book must sign the transaction

If a Key Book URL is used the Key Book is a Delegate, because the signing power and how the transactions are signed is up to the Key Book owner.

When adding a Key Book to a Key Page, the owner of the Key Book URL must sign a transaction to approve the addition of their Key Book to the Key Page.

_\*The Delegate can exist within the root ADI or a different ADI_

&#x20;__&#x20;

Key Page Rules for “UpdateKeyPage”:

1\.     A Key can modify its own entry or a Key of a different entry

2\.     A Key can modify a Delegate in its own entry or of a different entry

3\.     A Key can modify both a Key and Delegate in its own entry or of a different entry

4\.     A Delegate can modify its own entry or a Key of a different entry

5\.     A Delegate can modify a Delegate in its own entry or of a different entry

6\.     A Delegate can modify both a Key and Delegate in its own entry or of a different entry

7\.     A Key Page cannot Self-Delegate Authority to the Key Book the Key Page belongs to

8\.     Removing a Delegate does not require the approval of the Delegate. Only adding and updating requires approval.

&#x20;

There are many options available for Adding, Updating, and removing entries within a Key Page.\
Below are a few examples which illustrate multiple entries in a Key Page contain Delegates and Public Key Hashes.

&#x20;

**Signing with a Delegate**

If a Delegate is specified in a Key Page Entry, the Delegate can use any entry within its Key Book to sign a transaction with. If the Delegate is of a different ADI (remote), the signing key must be specified using  \[keyname@remotedelegatekeypage]. In the example below, the Delegate is remote.

&#x20;

./accumulate tx create \[adi token account] \[delegate signature] --delagator \[delegator key page] \[recipient]\[amount]

./accumulate tx create keybooktest.acme/token2 ben@keybooktest.acme/keybook2 --delegator keybooktest.acme/keybook/1 acc://ea9b01213430a8b3150db607789dd5c5c1aa45fdf39bc001/ACME 100

&#x20;

&#x20;       Transaction Hash        : 58589bc4521e9fcfec62e878797767449e13338e1954c64f625a2e077be0e1cc

&#x20;       Signature 0 Hash        : 1b8415021629ed7711675ddb597d790ae9ca1e861cd7eb2133c19b348328e340

&#x20;       Simple Hash             : 639e2d2c644c9b7951ebed616d8d239fe62daba81c6d0b7f4eaebc43c53c66a6

&#x20;       Error code              : ok

&#x20;       Result                  :

&#x20;****&#x20;

**Adding a Delegate and Public Key hash of a Key Page Entry**\
_\*The Public Key Hash is derived from theSHA256 Hash of the Public Key_

tx execute ./accumulate tx execute \[Key Page] \[Signing Key] '{type: updateKeyPage, operation: \[{ type: add, entry: { owner: \[Delegate], keyHash: \[Public Key Hash]} }]}'

&#x20;

./accumulate tx execute Delegatetest.acme/Keybook/1 newkey '{type: updateKeyPage, operation: \[{ type: add, entry: { owner: acc://Delegatetest.acme/Keybook3, keyHash: d2aad80e11d0478015c51c197e2df99da3a2c3309fb4245efa370a7033cdc127 } }]}'

&#x20;

&#x20;       Transaction Hash        : 619ec91821f0fec89a77d69ed1272f86e18fc70d78101660b4859f67f77fb90b

&#x20;       Signature 0 Hash        : 3533879d4a34f614c80c4fddb5aaebd0fabc676f2610c5199fd6a4f697f4a163

&#x20;       Simple Hash             : 42c71a77f5bc035d263887e052aa8e26911e92f07c6e025a8f3d94d2ae4eaf27

&#x20;       Error code              : ok

&#x20;       Result                  :

&#x20;

**Sign Transaction with Delegate**

./accumulate tx sign \[Key Book]\[Singing Key]\[Transaction ID]

./accumulate tx sign acc://Delegatetest.acme/Keybook3 newkey 619ec91821f0fec89a77d69ed1272f86e18fc70d78101660b4859f67f77fb90b

Transaction Hash        : 619ec91821f0fec89a77d69ed1272f86e18fc70d78101660b4859f67f77fb90b\
&#x20;   Signature 0 Hash        : fe1290db52481dfc99380a576a6db00dbdec588b37bc7e867e2a6f3493dc6206\
&#x20;   Simple Hash             : eccd36490ce21d1436e0d3b109922667a4f89f62f8247acd1f0dbce8ab413e31\
&#x20;   Error code              : ok\
&#x20;   Result                  :

&#x20;

**Query Key Page**

./accumulate get \[Key Page]

./accumulate get acc://Delegatetest.acme/Keybook/1

Credit Balance  :       999794.00\
\
&#x20;   Index  Nonce                          Key Name  Delegate                    Public Key Hash\
&#x20;   0      1969-12-31 19:00:00 -0500 EST            Delegatetest.acme/Keybook2\
&#x20;   1      1969-12-31 19:00:00 -0500 EST  newkey                                785b7f22ab201ae3f391cc47b06e2da00bbd47e7600ba1c68ea2cdb2b26f00ef\
&#x20;   2      1969-12-31 19:00:00 -0500 EST  newkey2   Delegatetest.acme/Keybook3  d2aad80e11d0478015c51c197e2df99da3a2c3309fb4245efa370a7033cdc127

&#x20;****&#x20;

**Updating a Delegate and Publick Key Hash of a Key Page Entry (Signing with a Delegate)**

./accumulate tx execute acc://Delegatetest.acme/Keybook/1 \[Signing Key]'{type: updateKeyPage, operation: \[{ type: update, oldEntry: {keyHash: \[Public Key Hash], Delegate: \[Delegate Key Book]} , newEntry: {keyHash: \[Public Key Hash], Delegate: \[Delegate Key Book]} \}}]}'

&#x20;****&#x20;

./accumulate tx execute acc://Delegatetest.acme/Keybook/1 newkey@Delegatetest.acme/Keybook3/1 '{type: updateKeyPage, operation: \[{ type: update, oldEntry: {keyHash: 39c2ada31c6cb824e80f2a96f17e077a7edc9f02a93d34eede2616a5c9c3412c, Delegate: Delegatetest.acme/Keybook3} , newEntry: {keyHash: 785b7f22ab201ae3f391cc47b06e2da00bbd47e7600ba1c68ea2cdb2b26f00ef, Delegate: Delegatetest.acme/Keybook3\}}]}' --delegator acc://Delegatetest.acme/Keybook/1

&#x20;

Transaction Hash        : 139c736cbccfc146d7731694d3a146417ef39be59614d63da9795d56307d38fc\
&#x20;   Signature 0 Hash        : 772207a552c99e43193992617686bd30c3ecaad790cc3952eaf25e3116ee5715\
&#x20;   Simple Hash             : 17a4e1591126c98eb9c0080444d109d18110a8366f3365a4f11fc9741b304567\
&#x20;   Error code              : ok\
&#x20;   Result                  :

&#x20;

**Sign Transaction with Delegate**

./accumulate tx sign \[Key Book]\[Signing Key]\[Transaction ID]

./accumulate tx sign acc://Delegatetest.acme/Keybook3 newkey 619ec91821f0fec89a77d69ed1272f86e18fc70d78101660b4859f67f77fb90b

Transaction Hash        : 139c736cbccfc146d7731694d3a146417ef39be59614d63da9795d56307d38fc\
&#x20;   Signature 0 Hash        : fe1290db52481dfc99380a576a6db00dbdec588b37bc7e867e2a6f3493dc6206\
&#x20;   Simple Hash             : eccd36490ce21d1436e0d3b109922667a4f89f62f8247acd1f0dbce8ab413e31\
&#x20;   Error code              : ok\
&#x20;   Result                  :

**Query Key Page**

./accumulate get acc://Delegatetest.acme/keybook/1

Credit Balance  :       999535.00\
\
&#x20;   Index  Nonce                          Key Name  Delegate                    Public Key Hash\
&#x20;   0      1969-12-31 19:00:00 -0500 EST            Delegatetest.acme/Keybook2\
&#x20;   1      1969-12-31 19:00:00 -0500 EST            Delegatetest.acme/Keybook4\
&#x20;   2      1969-12-31 19:00:00 -0500 EST            Delegatetest.acme/Keybook5\
&#x20;   3      1969-12-31 19:00:00 -0500 EST  newkey    Delegatetest.acme/Keybook3  785b7f22ab201ae3f391cc47b06e2da00bbd47e7600ba1c68ea2cdb2b26f00ef

&#x20;

**Removing a Delegate and Public Key Hash of a Key Page Entry**

./accumulate tx execute acc://Delegatetest.acme/Keybook/1 \[Signing Key] '{type: updateKeyPage, operation: \[{ type: remove, entry: { owner: \[Delegate Key Book], keyhash: \[Public Key Hash\}}]}'

&#x20;****&#x20;

./accumulate tx execute acc://Delegatetest.acme/Keybook/1 newkey4 '{"type": "updateKeyPage", "operation": \[{ "type": "remove", "entry": { "owner": "acc://Delegatetest.acme/Keybook7", "keyhash": "1071cce6eb3ffe8ff0739ee669d0f7b8d095095c088123ebe8039478ae2043fe"\}}]}'

Transaction Hash        : d2a93317575373327b3ba359ff7131d357fe3bbc4d05623a6e38ed23d2b1e35f\
&#x20;   Signature 0 Hash        : 2e64be2a1943017776ecdd9949876204b08ebde14ffdb4e832cc48f8ba4b546b\
&#x20;   Simple Hash             : 1d8f86444849e054f4286f10286ef8ebb9278ad19ed799eed68646896754617e\
&#x20;   Error code              : ok\
&#x20;   Result                  :

**Query Key Page**

./accumulate get acc://Delegatetest.acme/keybook/1

Credit Balance  :       999535.00\
\
&#x20;   Index  Nonce                          Key Name  Delegate                    Public Key Hash\
&#x20;   0      1969-12-31 19:00:00 -0500 EST            Delegatetest.acme/Keybook2\
&#x20;   1      1969-12-31 19:00:00 -0500 EST            Delegatetest.acme/Keybook4\
&#x20;   2      1969-12-31 19:00:00 -0500 EST            Delegatetest.acme/Keybook5\
&#x20;   3      1969-12-31 19:00:00 -0500 EST  newkey    Delegatetest.acme/Keybook3  785b7f22ab201ae3f391cc47b06e2da00bbd47e7600ba1c68ea2cdb2b26f00ef

&#x20;

&#x20;

**Multi-Signature with Delegates and Public Key Hash**

**Key Page Threshold is 3 of 3**

./accumulate get keybooktest.acme/keybook/1

&#x20;

&#x20;       Credit Balance  :       9540.98

&#x20;

&#x20;       Index  Nonce                                 Key Name  Delegate                   Public Key Hash

&#x20;       0      1969-12-31 19:00:00 -0500 EST                   Keybooktest.acme/Keybook2

&#x20;       1      1969-12-31 19:00:00 -0500 EST                   Keybooktest.acme/Keybook3

&#x20;       2      2022-06-30 17:28:39.849066 -0400 EDT  ben                                  0a1b1dae9e9dcc57cf010d420f026761599939a1be536d29e63a2a90a44dff3b

&#x20;

./accumulate tx create keybooktest.acme/token2 [ben@keybooktest.acme/keybook2](mailto:ben@keybooktest.acme/keybook2) --delegator keybooktest.acme/keybook/1 acc://ea9b01213430a8b3150db607789dd5c5c1aa45fdf39bc001/ACME 100

&#x20;

&#x20;       Transaction Hash        : ee7e9fa756757c17565622c0fd30dc71901f55d468285b2e8ff9271eb4686294

&#x20;       Signature 0 Hash        : ee21519f1563a4afe2f6369e19f8af602ec03f726ca5ae2678097c6b6ae7da12

&#x20;       Simple Hash             : b6c20c73c424a3b56d0ae40f931239d4133c6ce67cc8d94ae008f270d3b74ece

&#x20;       Error code              : ok

&#x20;       Result                  :

&#x20;

./accumulate tx sign keybooktest.acme/token2 [ben@keybooktest.acme/keybook3](mailto:ben@keybooktest.acme/keybook3) --delegator keybooktest.acme/keybook/1 ee7e9fa756757c17565622c0fd30dc71901f55d468285b2e8ff9271eb4686294

&#x20;

&#x20;       Transaction Hash        : ee7e9fa756757c17565622c0fd30dc71901f55d468285b2e8ff9271eb4686294

&#x20;       Signature 0 Hash        : 4fb819965f3441c48b43db8aace7198f52cbd70073faeccb9ac838912ca89bcf

&#x20;       Simple Hash             : d634638af2cb6a5ca08232675ed81a370350db1ef8f080d30bc4279e05402417

&#x20;       Error code              : ok

&#x20;       Result                  :

&#x20;

./accumulate tx sign keybooktest.acme/token2 ben ee7e9fa756757c17565622c0fd30dc71901f55d468285b2e8ff9271eb4686294

&#x20;

&#x20;       Transaction Hash        : ee7e9fa756757c17565622c0fd30dc71901f55d468285b2e8ff9271eb4686294

&#x20;       Signature 0 Hash        : 7c2d353429150c50be1cb6f5e9267a07f6acdba81a970d02aa035aeaf5aae1e3

&#x20;       Simple Hash             : aa75f3204fbb8f66ef8bd7f00f60eb09b4db845b2ea55991d736ff0bb2afe483

&#x20;       Error code              : ok

&#x20;       Result                  :

&#x20;

./accumulate get acc://ea9b01213430a8b3150db607789dd5c5c1aa45fdf39bc001/ACME

&#x20;

&#x20;       Account Url     :       acc://ea9b01213430a8b3150db607789dd5c5c1aa45fdf39bc001/ACME

&#x20;       Token Url       :       acc://ACME

&#x20;       Balance         :       1979999.40000000 ACME

&#x20;       CreditBalance   :       994.00

&#x20;       Last Used On    :       2022-06-30 13:30:29.04647 -0400 EDT

&#x20;****&#x20;

&#x20;****&#x20;

**Key Book Authorities**

In the same manner that a Key Book is the primary authority used to execute transactions for a given account, additional Key Books can be added as authorities. A Key Book Authority can either belong to a Key Book that exists within the same root ADI, or of a different ADI. When a Key Book Authority is added to an Account the Key Book signs a pending transaction for approval. A Key Book can be an authority to all account types except for Lite Token Lite Data Accounts, and Key Pages.\As a note, disabling an authority only means that the authority is not required to sign a transaction, but the option is still available.

&#x20;

Usage:

&#x20; accumulate auth \[command]

&#x20;

Aliases:

&#x20; auth, manager

&#x20;

Available Commands:

&#x20; add         Add an authority to an account

&#x20; disable     Disable authorization checks for an authority of an account

&#x20; enable      Enable authorization checks for an authority of an account

&#x20; remove      Remove an authority from an account

&#x20;

**Add an Authority**

When adding an Authority, the Authority must sign the transaction hash to approve its addition.

&#x20;

accumulate auth add \[account url] \[signing key name] \[key index (optional)] \[key height (optional)] \[authority url] \[flags]

./accumulate auth add acc://DefiDevs.acme/Tokens Key2 acc://DefiDevs.acme/Keybook2

&#x20;

&#x20;       Transaction Hash        : 45171d54df1058d4766c353c12255c41875ac57ccaba44020af548eddc3aa0d9

&#x20;       Signature 0 Hash        : c387c89886172288f39c14256c558c677be376013987ef3eb5888b9f064148a1

&#x20;       Simple Hash             : 3da6716ca5915c47bbd180cf37d5359ffc4d79351f20c9f45ca5eb3d367955df

&#x20;       Error code              : ok

&#x20;       Result                  :

&#x20;

./accumulate tx sign &#x20;

Usage:

&#x20; accumulate tx sign \[origin url] \[signing key name] \[key index (optional)] \[key height (optional)] \[txid]      Sign a pending transaction

\
\


./accumulate tx sign acc://DefiDevs.acme/Tokens acc://Key3@DefiDevs.acme/Keybook2 45171d54df1058d4766c353c12255c41875ac57ccaba44020af548eddc3aa0d9

Error:

&#x20;       Transaction Hash        : 45171d54df1058d4766c353c12255c41875ac57ccaba44020af548eddc3aa0d9

&#x20;       Signature 0 Hash        : 19067f8180ab3ba62ba51e9f01e780fc91d144369e3dbc6663ae792e17ea8734

&#x20;       Simple Hash             : 36e8292247f68013081b225d221586439736b7a0fbffb6b6771cf7940430478f

&#x20;       Error code              : 4

&#x20;       Error                   : transaction 45171D54 has been delivered

&#x20;       Result                  :

&#x20;

**A get command on the Token Account shows the two Key Book Authorities**

./accumulate get acc://DefiDevs.acme/Tokens

&#x20;

&#x20;       Account Url     :       acc://DefiDevs.acme/Tokens

&#x20;       Token Url       :       acc://ACME

&#x20;       Balance         :       85.00000000 ACME

&#x20;       Key Book Url    :       acc://DefiDevs.acme/Keybook

&#x20;       Key Book Url    :       acc://DefiDevs.acme/Keybook2

&#x20;

**Disable an Authority**

To disable an Authority, the Authority you are disabling must sign the transaction for approval. Although an Authority may be disabled it can still sign transactions, but the execution of the transaction is not dependent on the Disabled Authority. In addition, in order to update the Authority set a Disabled Authority must sign a transaction for approval.

&#x20;

accumulate auth disable \[account url] \[signing key name] \[key index (optional)] \[key height (optional)] \[authority url or index

(1-based)] \[flags]

&#x20;

./accumulate auth disable acc://DefiDevs.acme/Tokens acc://Key3@DefiDevs.acme/Keybook2 acc://DefiDevs.acme/Keybook2      &#x20;

&#x20;

&#x20;       Transaction Hash        : 1473f62845bfc30974b7c87b9c885d81bf2ca6e963c5f9bb2b12428af52538ae

&#x20;       Signature 0 Hash        : b362f8a9abea3a177f7540102911c461a5fedbdbb1a53cb3ae7c297b119b5bb8

&#x20;       Simple Hash             : 54fc208aa6dd08c0983376d1e0886ee82a9636e5b850ae5576458ab7cf9fc47a

&#x20;       Error code              : ok

&#x20;       Result                  :

&#x20;

./accumulate tx sign acc://DefiDevs.acme/Tokens acc://Key2@DefiDevs.acme/Keybook 1473f62845bfc30974b7c87b9c885d81bf2ca6e963c5f9bb2b12428af52538ae

&#x20;

&#x20;       Transaction Hash        : 1473f62845bfc30974b7c87b9c885d81bf2ca6e963c5f9bb2b12428af52538ae

&#x20;       Signature 0 Hash        : 4cb6383ac9831080cbd12e11b725a6809eebf9613376aa4096157867ef623ccc

&#x20;       Simple Hash             : 9e284ea79f47e15762ab8bae27c0952ff63c9f20cb3fdb0fcfde34ffddcb2d32

&#x20;       Error code              : ok

&#x20;       Result                  :

&#x20;****&#x20;

**Enable an Authority**

Enabling a Disabled Authority also requires a signature from the Disabled Authority.

accumulate auth enable \[account url] \[signing key name] \[key index (optional)] \[key height (optional)] \[authority url or index (1-based)] \[flags]

./accumulate auth enable acc://DefiDevs.acme/Tokens Key2 acc://DefiDevs.acme/Keybook2

&#x20;

&#x20;       Transaction Hash        : 76a62919ad23b8e9f790af52f78960787055a5376a2b7f4e747e9def63a6f892

&#x20;       Signature 0 Hash        : b9b1735969bd711a190d0c8a84d2c6587c0036e680183177fc5c69b920e75f26

&#x20;       Simple Hash             : f645f3c5fc414d41bf2ed53bb6bff3203929269ed6ebcaeac653cdabeab5dfc7

&#x20;       Error code              : ok

&#x20;       Result                  :

&#x20;

./accumulate tx sign acc://DefiDevs.acme/Tokens acc://Key2@DefiDevs.acme/Keybook 76a62919ad23b8e9f790af52f78960787055a5376a2b7f4e747e9def63a6f892

&#x20;

&#x20;       Transaction Hash        : 1473f62845bfc30974b7c87b9c885d81bf2ca6e963c5f9bb2b12428af52538ae

&#x20;       Signature 0 Hash        : 4cb6383ac9831080cbd12e11b725a6809eebf9613376aa4096157867ef623ccc

&#x20;       Simple Hash             : 9e284ea79f47e15762ab8bae27c0952ff63c9f20cb3fdb0fcfde34ffddcb2d32

&#x20;       Error code              : ok

&#x20;       Result                  :

&#x20;

**Remove an Authority**

Whether a Key Book is enabled or disabled, updating the authority set requires a signature from the Key Book being removed.

&#x20;****&#x20;

accumulate auth remove \[account url] \[signing key name] \[key index (optional)] \[key height (optional)] \[authority url or index (1-based)] \[flags]

&#x20;

./accumulate auth remove acc://DefiDevs.acme/Tokens Key2 acc://DefiDevs.acme/Keybook2

&#x20;

&#x20;       Transaction Hash        : de14677e318310c19c56fdc12aa7fbf6201c91bc851739c00de8636f28591569

&#x20;       Signature 0 Hash        : c8099cc81b5877376c02b9669b501dd0b9c139a65bddee68fae28a5bc7a766d0

&#x20;       Simple Hash             : e8912ec4e9104f4396303520d078d3357b034c0c988607ea5ebbd89fd93580af

&#x20;       Error code              : ok

&#x20;       Result                  :

&#x20;

./accumulate tx sign acc://DefiDevs.acme/Tokens acc://Key3@DefiDevs.acme/Keybook2 de14677e318310c19c56fdc12aa7fbf6201c91bc851739c00de8636f28591569

&#x20;

&#x20;       Transaction Hash        : de14677e318310c19c56fdc12aa7fbf6201c91bc851739c00de8636f28591569

&#x20;       Signature 0 Hash        : c01d0c4fb9cbcce99e5441f2b51d15dd9e7c8e56f3855dbb880ff1bd693bb1f5

&#x20;       Simple Hash             : c3921c1777dd12d591929be7309da166ed42f2f9fc236e85e5c083b6fead773e

&#x20;       Error code              : ok

&#x20;       Result                  :

&#x20;

**A get command on the Token Account shows the two Key Book Authorities**

./accumulate get acc://DefiDevs.acme/Tokens

&#x20;

&#x20;       Account Url     :       acc://DefiDevs.acme/Tokens

&#x20;       Token Url       :       acc://ACME

&#x20;       Balance         :       85.00000000 ACME

&#x20;       Key Book Url    :       acc://DefiDevs.acme/Keybook

&#x20;

**Multi-Signature with Multiple Authorities and Delegates and a Public Key Hash on Key Page**

./accumulate get acc://Keybooktest.acme/token2

&#x20;

&#x20;       Account Url     :       acc://keybooktest.acme/token2

&#x20;       Token Url       :       acc://ACME

&#x20;       Balance         :       9700.00000000 ACME

&#x20;       Key Book Url    :       acc://Keybooktest.acme/keybook

&#x20;       Key Book Url    :       acc://Keybooktest.acme/keybook5

&#x20;

./accumulate get acc://Keybooktest.acme/keybook/1

&#x20;

&#x20;       Credit Balance  :       9537.98

&#x20;

&#x20;       Index  Nonce                                 Key Name  Delegate                   Public Key Hash

&#x20;       0      1969-12-31 19:00:00 -0500 EST                   Keybooktest.acme/Keybook2

&#x20;       1      1969-12-31 19:00:00 -0500 EST                   Keybooktest.acme/Keybook3

&#x20;       2      2022-06-30 17:33:56.785636 -0400 EDT  ben                                  0a1b1dae9e9dcc57cf010d420f026761599939a1be536d29e63a2a90a44dff3b

&#x20;

./accumulate tx create keybooktest.acme/token2 ben@keybooktest.acme/keybook2 --delegator keybooktest.acme/keybook/1 acc://ea9b01213430a8b3150db607789dd5c5c1aa45fdf39bc001/ACME 100

&#x20;

&#x20;       Transaction Hash        : ff47923cfe657f184640ae6223cf50fc0b5238f47b4f7710c4b016ea372590b3

&#x20;       Signature 0 Hash        : b3e0048f87b99a2828371825fd2fcce41e9f0c7f3fc59f43af0ea5f045708448

&#x20;       Simple Hash             : 1d4b8827d655fd1f1e050c5f5073fe5acccedbd7216a363f109eeaf374bfa62f

&#x20;       Error code              : ok

&#x20;       Result                  :

&#x20;

./accumulate tx sign keybooktest.acme/token2 ben@keybooktest.acme/keybook3 --delegator keybooktest.acme/keybook/1 ff47923cfe657f184640ae6223cf50fc0b5238f47b4f7710c4b016ea372590b3

&#x20;

&#x20;       Transaction Hash        : ff47923cfe657f184640ae6223cf50fc0b5238f47b4f7710c4b016ea372590b3

&#x20;       Signature 0 Hash        : 7d4f3665874379b19db87fadd195b7967de83816ad1e6945fcd23c06d8ab9a99

&#x20;       Simple Hash             : 346547af6c7c65edca97f03864f71039a57e5a9341f5163de05ccb7ee20e5914

&#x20;       Error code              : ok

&#x20;       Result                  :

&#x20;****&#x20;

./accumulate tx sign keybooktest.acme/keybook5/1 ben ff47923cfe657f184640ae6223cf50fc0b5238f47b4f7710c4b016ea372590b3

&#x20;

&#x20;       Transaction Hash        : ff47923cfe657f184640ae6223cf50fc0b5238f47b4f7710c4b016ea372590b3

&#x20;       Signature 0 Hash        : 95126566fce72d0ad6a9805fdcf38ef34a5a49f1cbcc13a8994facbfedbaf101

&#x20;       Simple Hash             : 517766c67c712c803fc5c095e33d368b9ea1884854385f25b07f0e95b46b2c1e

&#x20;       Error code              : ok

&#x20;       Result                  :

&#x20;****&#x20;

**Sub-ADI and Sub-Sub-ADIs**

A Sub-ADI is an ADI created within an ADI. An example could be an organization that creates an ADI and different departments within the origination are Sub-ADIs. It is important to note that a Sub-ADI can inherit the parent's authority set if specified (KeyBooks). Meaning the sub-ADI's authority set will be set to a copy of the parent's Key Books and the contents within those Key Books. Any future modification to the parent ADI will not influence the Sub-ADI. When creating a Sub-ADI, you can create a new Key Book for the Sub-ADI. When creating accounts within the Sub-ADI the only material difference is that instead of referencing the ADI URL you reference the Sub-ADI URL. Sub-ADIs can have a subordinate ADI or Sub-Sub ADI which can also have a subordinate ADI. Everything in moderation including moderation. An ADI, Sub ADI, or Sub Sub-ADI can only sign transactions using the Key Page within the ADI, Sub ADI or Sub Sub ADI.

For the “ADI URL to Create” argument you would specify the Sub-ADI.

Acc://\<ADI Name>/\<Sub ADI Name>/\<Keybook (optional)>

&#x20;accumulate adi create \[origin-adi-url] \[wallet signing key name] \[key index (optional)] \[key height (optional)] \[adi url to create] \[public key or wallet key name] \[key book url (optional)] \[public key page 1 (optional)] Create new ADI for another ADI

&#x20;

./accumulate adi create acc://DefiDevs.acme Key2 acc://DefiDevs.acme/Car Key2 acc://DefiDevs.acme/Car/Keybook

&#x20;

&#x20;       Transaction Hash        : 5b94f5c9a7b19cc2c519116c9019848df4de4fb31be0e5adf6c99802ab8683c2

&#x20;       Signature 0 Hash        : 98a2bfb209e63da0be9d945cf8538555c5cac25d8a706ebe73d8070002b20de2

&#x20;       Simple Hash             : 730ca4e3f825d078b219afbfae2ae50ffc382a736a86d3ae865e8f5b3d4ac713

&#x20;       Error code              : ok

&#x20;       Result                  :

&#x20;

&#x20;

**Adding Credits to a Sub-ADI Key Page**

./accumulate credits acc://f338762f7013acb0fd5e1480c20df47ff836862adbd6e0f1/ACME acc://DefiDevs.acme/Car/Keybook/1 10000

&#x20;

&#x20;       Transaction Hash        : c6eabf824a4710ad427306b4f0f72158f76a6d1ddda5d15c5ff7f5d3ae048a63

&#x20;       Signature 0 Hash        : 05470466229b5747ce2c80e6dfd6176d0701e3e893dfc7408c9caa824a51ee21

&#x20;       Simple Hash             : fbe8ba8ba462ec7edbed869a1e86036ac48db2230347b0e060b109e125c36943

&#x20;       Error code              : ok

&#x20;       Result                  : Oracle        $0.05 / ACME

&#x20;                                 Credits       10000.00

&#x20;                                 Amount        2000.00000000 ACME

&#x20;

**Add Credits to a Sub-ADI Key Page**

PS C:\Users\stolm\accumulated> ./accumulate get acc://DefiDevs.acme/Car/Keybook/1

&#x20;

&#x20;       Credit Balance  :       10000.00

&#x20;

&#x20;       Index   Nonce           Public Key                                                              Key Name(s)

&#x20;       0       1969-12-31 19:00:00 -0500 EST           f619aa889a2532d2d331d8a1287895b87605d7a5a1c75ad671f9bb6a7628940c        Key2

&#x20;

**Create a Sub-Sub-ADI**

In the example below, the Origin ADI URL is the Sub-ADI and the ADI URL to create is the Sub-Sub-ADI

accumulate adi create \[origin-adi-url] \[wallet signing key name] \[key index (optional)] \[key height (optional)] \[adi url to create] \[public key or wallet key name] \[key book url (optional)] \[public key page 1 (optional)] Create new ADI for another ADI

./accumulate adi create acc://DefiDevs.acme/Robot Key2 acc://DefiDevs.acme/Robot/MrRoboto Key2

&#x20;

&#x20;       Transaction Hash        : 0c681b2bdf1c3608a675bb8a6111040979b33fb6c7f049c2fc31fe7ebb4dca31

&#x20;       Signature 0 Hash        : 5190c67a22f61c53bba47cd9d8e081c971900c0d6b5bebf96468907646b5c2d4

&#x20;       Simple Hash             : 971debec83777998f35715ba640429de57a4dc70b593997c6e10bd8a2f38a5cf

&#x20;       Error code              : ok

&#x20;       Result                  :

&#x20;****&#x20;

**ADI Token Account**

An ADI can have different account types such as an ADI Token Account. An ADI can have multiple ADI Token Accounts, but each ADI token account can only hold one type of token such as ACME, Accumulate’s native token. An ADI assigns Key Books to accounts that it creates. As an example, when a Token Account is created it is assigned a Key Book that the ADI has created. For creating credits for an ADI (which will be stored in a Key Page) an ADI Token Account can be referenced as the sponsor. The above is true for Sub-ADIs. In the matrix below the token accounts can be in the same ADI or different ADIs.

&#x20;

| <p> </p><p><strong>Token Account</strong> </p><p> </p><p>Sender/Receiver</p><p> </p> | <p> </p><p>Lite Token Account</p><p> </p> | <p> </p><p>ADI Token Account</p><p> </p> | <p> </p><p>Sub-ADI Token Account</p><p> </p> |
| ------------------------------------------------------------------------------------ | ----------------------------------------- | ---------------------------------------- | -------------------------------------------- |
| <p> </p><p>Lite Token Account</p><p> </p>                                            | <p> </p><p>X</p><p> </p>                  | <p> </p><p>X</p><p> </p>                 | <p> </p><p>X</p><p> </p>                     |
| <p> </p><p>ADI Token Account</p><p> </p>                                             | <p> </p><p>X</p><p> </p>                  | <p> </p><p>X</p><p> </p>                 | <p> </p><p>X</p><p> </p>                     |
| <p> </p><p>Sub-ADI Token Account</p><p> </p>                                         | <p> </p><p>X</p><p> </p>                  | <p> </p><p>X</p><p> </p>                 | <p> </p><p>X</p><p> </p>                     |

&#x20;

This matrix doesn’t capture sub-sub ADI token accounts and sub-sub-sub ADI Token accounts etc.

&#x20;****&#x20;

accumulate account create token \[actor adi] \[signing key name] \[key index (optional)] \[key height (optional)] \[new token account url] \[tokenUrl] \[keyBook (optional)] \[flags]

&#x20;****&#x20;

./accumulate account create token acc://DefiDevs.acme Key1 acc://DefiDevs.acme/Tokens acc://ACME acc://DefiDevs.acme/Keybook&#x20;

&#x20;

&#x20;       Transaction Hash        : cb9e0d5d0c6b90395bf08deb1a048d9552dfa3a5e068318847a7d1573120c927&#x20;

&#x20;       Signature 0 Hash        : 9504352f6f0dcd467934f9497129468737bab04f9c10592fc15dd38b070a54ed&#x20;

&#x20;       Simple Hash             : c53950eff4d6f0a22e5bb72f231876ad1684b28a2a0f675ef3bf0deeef43c974&#x20;

&#x20;       Error code              : ok&#x20;

&#x20;       Result                  :&#x20;

&#x20;

**QR Codes**

Within the CLI QR codes can be generated for accounts such as a token account.

&#x20;****&#x20;

./accumulate account qr acc://DefiDevs.acme/Tokens

&#x20;

![](file:///Users/qisforq/Library/Group%20Containers/UBF8T346G9.Office/TemporaryItems/msohtmlclip/clip\_image001.jpg)

&#x20;

**Sub-ADI Token Account**

accumulate account create token \[actor adi] \[signing key name] \[key index (optional)] \[key height (optional)] \[new token account url] \[tokenUrl] \[keyBook (optional)] \[flags]

&#x20;****&#x20;

./accumulate account create token  acc://DefiDevs.acme/Robot Key2 acc://DefiDevs.acme/Robot/Tokens acc://ACME acc://DefiDevs.acme/Robot/book

&#x20;

&#x20;       Transaction Hash        : ab1bf8daa1513bd72a43d33dc5ee86d28d20ba8a275ae32a4340e512281816d1

&#x20;       Signature 0 Hash        : 7f511785d08be697f7775445778ab52070b0ba8291569aadfb07ac574eccd112

&#x20;       Simple Hash             : 9b2746b7a8adf4e52992d67015f4244aa2a07f9897c9c1391398d12c8a68862b

&#x20;       Error code              : ok

&#x20;       Result                  :

&#x20;****&#x20;

**Sending Tokens**

In the matrix provided above there are many ways to construct a transaction to send tokens.

accumulate tx create \[origin url] \[signing key name] \[key index (optional)] \[key height (optional)] \[to] \[amount]     Create new token tx

&#x20;

**Lite Token Account to Lite Token Account**

./accumulate tx create acc://27259b5544176ede283ba745b5a6d1775a281ad2f28abc3d/ACME acc://0143b52490530b90eef9b1a2405e322c6badc1e90e200c56/ACME 100

&#x20;

&#x20;       Transaction Hash        : 7661c348b839429d33b62964a69e8c7a7b48a57655eb0ba75dee6e62a6539e15

&#x20;       Signature 0 Hash        : 20bb93795e86b52a8379706b52121cc69a078b34a7bf0a542ba58446767a3bc1

&#x20;       Simple Hash             : 12eea88a2b11d2d198465ca5a3d235745b376a2e89538d0794edac377f8d5b91

&#x20;       Error code              : ok

&#x20;       Result                  :

&#x20;

**Lite Token Account to ADI Token Account**

./accumulate tx create acc://27259b5544176ede283ba745b5a6d1775a281ad2f28abc3d/ACME acc://DefiDevs.acme/Tokens 100                       &#x20;

&#x20;

&#x20;       Transaction Hash        : f3523717198218cdf68e0e1721dcbaaa0e26daa946ac0d444d6a2eb110d80766

&#x20;       Signature 0 Hash        : 5da4435ab9efb98121b83a6f0f82dfa182e67ac2e67506d5ab16c03dd926e970

&#x20;       Simple Hash             : 63b5804ea8978a3551b09ce9fd5735e3e467caad1ca0f83fbefc0d0bdabf1aba

&#x20;       Error code              : ok

&#x20;       Result                  :

&#x20;

**Lite Token Account to Sub-ADI Token Account**

./accumulate tx create acc://27259b5544176ede283ba745b5a6d1775a281ad2f28abc3d/ACME acc://DefiDevs.acme/Robot/Tokens 50

&#x20;

&#x20;

&#x20;       Transaction Hash        : dfc0e7985b39093905d3bbeba30a2c62f19e6a5831ab19eac23a806cc722a52a

&#x20;       Signature 0 Hash        : c91e7e0dc8af91a86479e52c2c594a3c6e805f719fce2fd3c7349db4f4d151ed

&#x20;       Simple Hash             : 2dee95a8ab0fc3aaaf1d9dbd15bc98e6bb4620d9968c99bc0e7e90e981ba0b48

&#x20;       Error code              :

&#x20;

**Note: The signing Key used to sign ADI related token transactions must be specified.**

&#x20;****&#x20;

**ADI Token Account to Lite Token Account**

./accumulate tx create acc://DefiDevs.acme/Tokens Key2 acc://27259b5544176ede283ba745b5a6d1775a281ad2f28abc3d/ACME 5

&#x20;

&#x20;

&#x20;       Transaction Hash        : 1a4df2b595cc31f6f757e746220a553e35f537657a0ed316a4a96efafef14b70

&#x20;       Signature 0 Hash        : 9c9e3c8fb538c9be02b95104ed5d250df952a928522b121a9e4a332f90b007b5

&#x20;       Simple Hash             : 53fb8484089d7d5446189b95fda6f13a596749cd05bf7152b3fa0f02a773d664

&#x20;       Error code              : ok

&#x20;       Result                  :

&#x20;****&#x20;

&#x20;****&#x20;

**ADI Token Account to ADI Token Account**

./accumulate tx create acc://Google.acme/Tokens Key5 acc://DefiDevs.acme/Tokens 50000

&#x20;

&#x20;       Transaction Hash        : b19693227a78e9a77b33c8ced3478859b546c5eb62432213ee166c244c82c9b3

&#x20;       Signature 0 Hash        : fd62872f6b50d77ad2f7f5b1094044742753bef54b727cefcb9d374b81c93126

&#x20;       Simple Hash             : afbd3cd9446cf8e2d330ad0196885b97e4b24117b37a97481c420ef3364dfa11

&#x20;       Error code              : ok

&#x20;       Result                  :

&#x20;

**ADI Token Account to Sub-ADI Token Account**

./accumulate tx create acc://Google.acme/Tokens Key5 acc://DefiDevs.acme/Robot/Tokens 50000

&#x20;

&#x20;       Transaction Hash        : e4c365656e79f2e32d8437e6d1d506a7af3f0dbb1e7b66be88c3b4733718d92d

&#x20;       Signature 0 Hash        : e9604249de1ce9ea24f260fba43614f300485f73b7ebb577649753dd256b5add

&#x20;       Simple Hash             : c4677739bafe5e0172d1cc809ac99f064ea44c1c20d0786b51acaf8b2581cc5d

&#x20;       Error code              : ok

&#x20;       Result                  :

&#x20;

**Sub-ADI Token Account to Lite Token Account**

./accumulate tx create acc://Google.acme/Car/Tokens Key5 acc://0143b52490530b90eef9b1a2405e322c6badc1e90e200c56/ACME 500     &#x20;

&#x20;

&#x20;       Transaction Hash        : c113830891189d6629ba3a805c4986b9b2982c3c2b8fd56a4c3885f6f5f67f17

&#x20;       Signature 0 Hash        : c00b898a3fad87c5409307ebe5fc4e36ec3a3b48591f098ac687a378a8fe6ad7

&#x20;       Simple Hash             : 07356e79eb4667006b59c29a9cbc87a3eaf454182d0fb03e462514376d7cfd33

&#x20;       Error code              : ok

&#x20;       Result                  :

&#x20;

**Sub-ADI Token Account to ADI Token Account**

./accumulate tx create acc://Google.acme/Car/Tokens Key5 acc://DefiDevs.acme/Tokens 500             &#x20;

&#x20;

&#x20;       Transaction Hash        : b2ee0db7c9ec0408422debd5ec97b6e117719a5214ae461ffce55883f9e2d81d

&#x20;       Signature 0 Hash        : 6a1b03cf932df5c7cf4e366c5d41c075a8854ab189b383555de5e1106ce33898

&#x20;       Simple Hash             : b94358ff85c232bfef3523e9ca2e466281a181769c3c039127c1641d3601d4a7

&#x20;       Error code              : ok

&#x20;       Result                  :

&#x20;

&#x20;

**Sub-ADI Token Account to Sub-ADI Token Account**

./accumulate tx create acc://Google.acme/Car/Tokens Key5 acc://DefiDevs.acme/Robot/Tokens 500       &#x20;

&#x20;

&#x20;       Transaction Hash        : 164521b1d09a3d3b75014e24afef6fd7caa1e1b73de17a61f07ba51ceb6568da

&#x20;       Signature 0 Hash        : d9615532fc9a5f23914ecddc2f7da94ed8066cb5928e12a8b0d9455595a50608

&#x20;       Simple Hash             : 4d22ca9d28da2ce87928e5735069427b4b418df2a646391192289e6165f19fe5

&#x20;       Error code              : ok

&#x20;       Result                  :

&#x20;****&#x20;

&#x20;****&#x20;

**Create a Token Issuer**

accumulate token create \[origin adi or lite url] \[adi signer key name (if applicable)] \[token issuer url]\[BS4]  \[symbol] \[precision (0 - 18)] \[supply limit] \[properties URL (optional)] \[flags]

Precision = number of decimal places after point

&#x20;

./accumulate token create acc://DefiDevs.acme Key2 acc://DefiDevs.acme/AI AI 1 100000000

&#x20;

&#x20;       Transaction Hash        : 1c3831173fbe09247386fa9630f80de13b160dfb7d2f8361dfb7a3e440a492d9

&#x20;       Signature 0 Hash        : ebaa7ebcd6a495d84b822bd8f70afe8c9b266321bc2955c3fdcba8a7eb9ebdbc

&#x20;       Simple Hash             : 469615f0d9f4a31cccc5b641e752892a43c1a03eab8cb11c8eee95d8d6254724

&#x20;       Error code              : ok

&#x20;       Result                  :

&#x20;****&#x20;

**Create a Custom ADI Token Account**

./accumulate account create token \[ADI URL]\[Signing Key]\[ADI Token Account]\[Token Issuer]

&#x20;

./accumulate account create token acc://DefiDevs.acme Key2 acc://DefiDevs.acme/AITokens acc://DefiDevs.acme/AI

&#x20;

&#x20;       Transaction Hash        : 131c29f769d2a7d7ce8701128dbdaf1c844f998259dcad011c01ed37442ec9c7

&#x20;       Signature 0 Hash        : 9bde03cfff80e951246523611cef2d716806efa4e3893c5ee5ecbdac7dea884f

&#x20;       Simple Hash             : 32e9f4894f76d519e979672c142c2ab453787dd93acedd313ed8527dbc19a9fa

&#x20;       Error code              : ok

&#x20;       Result                  :

&#x20;****&#x20;

**Issuing Tokens**

accumulate token issue \[adi token url] \[signer key name] \[recipient url] \[amount] \[flags]

./accumulate token issue acc://DefiDevs.acme/AI Key2 acc://DefiDevs.acme/AITokens 10000

&#x20;

&#x20;       Transaction Hash        : fdc8a0a1e243471b49bb071afc06eb90b14b5319a936e7738029b47593346da3

&#x20;       Signature 0 Hash        : 05f594fa041de539347d11362c0aea7a170519519eaf191ca5257a8168938bf8

&#x20;       Simple Hash             : 203c7045e3ddd1c7fa6e48d325f3d12022626d39aaf186defe489f152850cfa3

&#x20;       Error code              : ok

&#x20;       Result                  :

&#x20;

**Creating a Custom Lite Token Account by Issuing Tokens to it**

Append the TokenIssuer Account to the Lite Token Account Address to receive custom tokens.

./accumulate tx create acc://DefiDevs.acme/AITokens Key2 acc://0143b52490530b90eef9b1a2405e322c6badc1e90e200c56/DefiDevs.acme/AI 10

&#x20;

&#x20;       Transaction Hash        : 015515d4fea655d2f99af36adbdb4e9fdb7462b018d75916fb628ceadefe852b

&#x20;       Signature 0 Hash        : 2a14c86cd3e20d2917a5884c24c66d263633176b4c3b2d63b51bc8ecd6417273

&#x20;       Simple Hash             : 6e42d102fe9b29b226b3a48f0db1e9dd8a63c735e7db357d92e731609572dd5a

&#x20;       Error code              : ok

&#x20;       Result                  :

&#x20;****&#x20;

**Burn Tokens**

./accumulate token burn

&#x20; accumulate token burn \[adi or lite token account] \[adi signer key name (if applicable)] \[amount] \[flags]

&#x20;

**Burn Tokens from a Lite Token Account**

./accumulate token burn acc://0143b52490530b90eef9b1a2405e322c6badc1e90e200c56/ACME 10

&#x20;

&#x20;       Transaction Hash        : 3b873d31fcb1555dece4e07288c936cb97bd9b95fcdc4975367ac593f6dfed64

&#x20;       Signature 0 Hash        : a9281063dacd05fc5097a919d12a6498e7c3e339c77e970fb9832645e409daba

&#x20;       Simple Hash             : b0f13b056216effccad96f2b328a3c579b86f8df147a9535d196638ebfc6bc0e

&#x20;       Error code              : ok

&#x20;       Result                  :

&#x20;

**Burn Tokens from an ADI Token Account**

_A decimal value must be added (can be 0) when burning tokens_

./accumulate token burn acc://DefiDevs.acme/Tokens Key2 9\[BS5] .0

&#x20;

&#x20;       Transaction Hash        : e1e2ca605288e35a78d2413156e3d718f601330f2d0c684494099d301d1b97e2

&#x20;       Signature 0 Hash        : b11eba4bc508076d1b3e01d2eee40892eaccccc3d83efe17126b850c93057c8f

&#x20;       Simple Hash             : 26f5d0f163f677da0d840e2fbbd17ace0663fe44c8de2c207cd95fdd2e42b70a

&#x20;       Error code              : ok

&#x20;       Result                  :

&#x20;****&#x20;

**Create an ADI Data Account**

Create an ADI Data Account

&#x20; accumulate account create data \[actor adi url] \[signing key name] \[key index (optional)] \[key height (optional)] \[adi data account url] \[key book (optional)] Create new data account

&#x20;                example usage: accumulate account create data acc://actor signingKeyName acc://actor/dataAccount acc://actor/book0

&#x20;

./accumulate account create data  acc://DefiDevs.acme Key1 acc://DefiDevs.acme/Data acc://DefiDevs.acme/Keybook

&#x20;

&#x20;       Transaction Hash        : 55bf5c8fcb3603185e9c25f481d22843ff6c5a4398fa276d2764cdc91641a3f0

&#x20;       Signature 0 Hash        : 8ef47e055cf47b4152f7243d3cc2e9f970b3dde79af614b8c6718f76b71219f3

&#x20;       Simple Hash             : 0ad1a784211354d5893c25a42f7dabe5e02b65abbc3c57007add3a450c020bf8

&#x20;       Error code              : ok

&#x20;       Result                  :

&#x20;

**Write to an ADI Data Account**

accumulate data write \[data account url] \[signingKey] \[extid\_0 (optional)] ... \[extid\_n (optional)] \[data] Write entry to your data account. Note: extid's and data needs to be a quoted string or hex

&#x20;

./accumulate data write acc://DefiDevs.acme/data Key2 "entryhashtest1"

&#x20;

&#x20;       Entry Hash              :8de01ef68a5b5d667008f30e2099b8dd11120efc4fd1d21462521f68ab87d4bb

&#x20;       Transaction Hash        : f3c71bd6b6677f69ef87e98d966b705a75dec0f8e8dfed292bd39b09e2ee2969

&#x20;       Signature 0 Hash        : b0490493d82b23259672111ea5170ac19257a35b9de41d5278262eee7a326783

&#x20;       Simple Hash             : 1c30a9a75adf93268a23d034a43fd358958ad7a91f794ecf10f888c96f7d1121

&#x20;       Error code              : ok

&#x20;       Result                  : Account URL   acc://DefiDevs.acme/data

&#x20;                                 Account ID    dfe2c4ee93777ff5fb97e1d8f2ddd45336044e2a3396db8344a73b94e6fb0d45

&#x20;                                 Entry Hash    8de01ef68a5b5d667008f30e2099b8dd11120efc4fd1d21462521f68ab87d4bb

&#x20;

**Querying an ADI Data Account by URL**

accumulate data get \[DataAccountURL] Get most current data entry by URL

&#x20;

./accumulate data get acc://DefiDevs.acme/Data

{"type":"dataEntry","mainChain":{"height":4,"count":4,"roots":\["55bf5c8fcb3603185e9c25f481d22843ff6c5a4398fa276d2764cdc91641a3f0","7b58817aa8a52bce3ffd8c40e11322dc945e3debc365d5cc7204be9500b12b7d","19f66cbbfad4153c1481d88a6990604c6bc46aac176c6347e269f6f9ff7f49b2","f3c71bd6b6677f69ef87e98d966b705a75dec0f8e8dfed292bd39b09e2ee2969"]},"data":{"entry":{"data":\["656e747279686173687465737431"]},"entryHash":"8de01ef68a5b5d667008f30e2099b8dd11120efc4fd1d21462521f68ab87d4bb"},"chainId":"dfe2c4ee93777ff5fb97e1d8f2ddd45336044e2a3396db8344a73b94e6fb0d45"}

&#x20;

**Querying an ADI Data Account by URL and a Specific Entry Hash**

accumulate data get \[DataAccountURL] \[EntryHash]  Get data entry by entryHash in hex

&#x20;

./accumulate data get acc://DefiDevs.acme/Data 8de01ef68a5b5d667008f30e2099b8dd11120efc4fd1d21462521f68ab87d4bb

{"type":"dataEntry","mainChain":{"height":4,"count":4,"roots":\["55bf5c8fcb3603185e9c25f481d22843ff6c5a4398fa276d2764cdc91641a3f0","7b58817aa8a52bce3ffd8c40e11322dc945e3debc365d5cc7204be9500b12b7d","19f66cbbfad4153c1481d88a6990604c6bc46aac176c6347e269f6f9ff7f49b2","f3c71bd6b6677f69ef87e98d966b705a75dec0f8e8dfed292bd39b09e2ee2969"]},"data":{"entry":{"data":\["656e747279686173687465737431"]},"entryHash":"8de01ef68a5b5d667008f30e2099b8dd11120efc4fd1d21462521f68ab87d4bb"},"chainId":"dfe2c4ee93777ff5fb97e1d8f2ddd45336044e2a3396db8344a73b94e6fb0d45"}

&#x20;

**Querying an ADI Data Account by URL and a Specific Index**

accumulate data get \[DataAccountURL] \[start index] \[count] expand(optional) Get a set of data entries starting from start and going to start+count, if "expand" is specified, data entries will also be provided

&#x20;

./accumulate data get acc://DefiDevs.acme/Data 0 1

{"type":"dataSet","items":\[{"entry":{},"entryHash":"a6b54c20a7b96eeac1a911e6da3124a560fe6dc042ebf270e3676e7095b95652"}],"start":0,"count":1,"total":3}

&#x20;

**Write to an ADI Data Account (Scratch Chain)**

Write scratch data command:

./accumulate data write \[ADI Data Account]\[Signing Key]  --scratch \[data]

&#x20;

./accumulate data write DeFiDevs.acme/data 1d92f317cb3ed1b2992d345ae9546ec0d66c069c4b471c04 --scratch "DATA"

&#x20;

&#x20;   Entry Hash        :12e90b8e74f20fc0a7274cff9fcbae14592db12292757f1ea0d7503d30799fd2\
&#x20;    Transaction Hash    : 39890ec7018199c8a4186ecd20634e3a64c5d8e8c15835035689655d8d37e8ae\
&#x20;    Signature 0 Hash    : a30f0470c60bb21340de902609034d530694f6d81ca2ddf670bb98c1a349d675\
&#x20;    Simple Hash        : f9c49c07e7c0e2774fa9c22dfad5a5c100755b29f83cbffd53f84a059cc88787\
&#x20;    Error code        : ok\
&#x20;    Result            : Account URL    acc://StebbyWebby.acme/superData\
&#x20;                  Account ID    edb5a7e9186c418e3024cfa191d781929777470d21d7b2d4aa049f077737d589\
&#x20;                  Entry Hash    12e90b8e74f20fc0a7274cff9fcbae14592db12292757f1ea0d7503d30799fd2

&#x20;

&#x20;

**Create a Sub-ADI Data Account**

./accumulate account create data acc://DefiDevs.acme/Robot Key2 acc://DefiDevs.acme/Robot/Data acc://DefiDevs.acme/Robot/Book

&#x20;

&#x20;       Transaction Hash        : 9c60e74028f727337d60bf6239c5bfb1a46de9580a6d8c89b1bf184a9988da9b

&#x20;       Signature 0 Hash        : d64a914c3f63804d2c38bd79805091f2f0a8d2072e9cbd517bb022d18dfe4cbe

&#x20;       Simple Hash             : 1647fa7c763ec3b88aa9cb2e61cd28c1afed2ddffc869c9702bdbd8cb22c43df

&#x20;       Error code              : ok

&#x20;       Result                  :

&#x20;

**Write to a Sub-ADI Data Account**

accumulate data write \[data account url] \[signingKey] \[extid\_0 (optional)] ... \[extid\_n (optional)] \[data] Write entry to your data account. Note: extid's and data needs to be a quoted string or hex

&#x20;

./accumulate data write acc://Test.acme/SubADITest/Data Key1 'Key6'

&#x20;

&#x20;       Entry Hash              :2cf24dba5fb0a30e26e83b2ac5b9e29e1b161e5c1fa7425e73043362938b9824     &#x20;

&#x20;       Transaction Hash        : 1cda6093788c0d10a4f9ff0b8f135629388dc3446672147947ecd2c4a0c8c7a3    &#x20;

&#x20;       Signature 0 Hash        : 2a53c605b56fa09977ae8a3ad8ed170e38b1900c5961b31d72d4e62dd547743e    &#x20;

&#x20;       Simple Hash             : 6aaa93d3fe0830ff20943ab4911f40fdfd8611984e17ec9ec7aa21a956b70b97    &#x20;

&#x20;       Error code              : ok

&#x20;       Result                  : Account URL   acc://Test.acme/SubADITest/Data

&#x20;                                 Account ID    a3bd84932993317d8987cbc1ecccb0d230565feb55096cc1fc9ea3637d520942

&#x20;                                 Entry Hash    2cf24dba5fb0a30e26e83b2ac5b9e29e1b161e5c1fa7425e73043362938b9824

&#x20;

&#x20;

**Querying a Sub-ADI Data Account by URL**

accumulate data get \[DataAccountURL] Get most current data entry by URL

./accumulate data get acc://Test.acme/SubADITest/Data

{"type":"dataEntry","mainChain":{"height":2,"count":2,"roots":\[null,"d4b13e8793e57c63e8df020e07b13364d9404f1bfac83c183681cc59e6650a59"]},"data":{"entry":{"data":\["68656c6c6f"],"type":"accumulate"},"entryHash":"2cf24dba5fb0a30e26e83b2ac5b9e29e1b161e5c1fa7425e73043362938b9824"},"chainId":"a3bd84932993317d8987cbc1ecccb0d230565feb55096cc1fc9ea3637d520942"}

&#x20;

**Querying a Sub-ADI Data Account by URL and a Specific Entry Hash**

accumulate data get \[DataAccountURL] \[EntryHash]  Get data entry by entryHash in hex

./accumulate data get acc://Test.acme/SubADITest/Data 2cf24dba5fb0a30e26e83b2ac5b9e29e1b161e5c1fa7425e73043362938b9824

{"type":"dataEntry","mainChain":{"height":2,"count":2,"roots":\[null,"d4b13e8793e57c63e8df020e07b13364d9404f1bfac83c183681cc59e6650a59"]},"data":{"entry":{"data":\["68656c6c6f"],"type":"accumulate"},"entryHash":"2cf24dba5fb0a30e26e83b2ac5b9e29e1b161e5c1fa7425e73043362938b9824"},"chainId":"a3bd84932993317d8987cbc1ecccb0d230565feb55096cc1fc9ea3637d520942"}

&#x20;

**Querying a Sub-ADI Data Account by URL and a Specific Index**

accumulate data get \[DataAccountURL] \[start index] \[count] expand(optional) Get a set of data entries starting from start and going to start+count, if "expand" is specified, data entries will also be provided

./accumulate data get acc://Test.acme/SubADITest/Data 0 10             &#x20;

{"type":"dataSet","items":\[{"entry":null,"entryHash":"2cf24dba5fb0a30e26e83b2ac5b9e29e1b161e5c1fa7425e73043362938b9824"}],"start":0,"count":10,"total":1}

&#x20;

**Write to a Sub-ADI Data Account (Scratch Chain)**

./accumulate data write DeFiDevs.acme/subadi/data 1d92f317cb3ed1b2992d345ae9546ec0d66c069c4b471c04 --scratch "DATA"

&#x20;

&#x20;   Entry Hash        :12e90b8e74f20fc0a7274cff9fcbae14592db12292757f1ea0d7503d30799fd2\
&#x20;    Transaction Hash    : 39890ec7018199c8a4186ecd20634e3a64c5d8e8c15835035689655d8d37e8ae\
&#x20;    Signature 0 Hash    : a30f0470c60bb21340de902609034d530694f6d81ca2ddf670bb98c1a349d675\
&#x20;    Simple Hash        : f9c49c07e7c0e2774fa9c22dfad5a5c100755b29f83cbffd53f84a059cc88787\
&#x20;    Error code        : ok\
&#x20;    Result            : Account URL    acc://StebbyWebby.acme/superData\
&#x20;                  Account ID    edb5a7e9186c418e3024cfa191d781929777470d21d7b2d4aa049f077737d589\
&#x20;                  Entry Hash    12e90b8e74f20fc0a7274cff9fcbae14592db12292757f1ea0d7503d30799fd2

&#x20;****&#x20;

**Minor Blocks**

&#x20;****&#x20;

accumulate blocks minor \[subnet-url] \[start index] \[count] \[tx fetch mode expand|ids|countOnly|omit (optional)] \[filter synth-anchors only blocks true|false (optional)] Get minor blocks

&#x20;****&#x20;

**Directory Network Minor Blocks**

&#x20;****&#x20;

./accumulate blocks minor acc://dn 0 2

&#x20;

&#x20;       Minor block result Start: 0      Count: 2        Total: 0

\==========================================================================

\--- block #1, blocktime 2022-05-03 17:20:17 +0000 UTC:

&#x20;   total tx count      : 4

&#x20;   txid #1             : e43be90e349210456662d8b8bdc9cc9e5e46ccb07f2129e7b57a8195e5e916d5

&#x20;   txid #2             : c843452b4943c755c020ddc10b156fc78c712a187ce048f9036bda1703e03ef4

&#x20;   txid #3             : 0b6c57a48522f77d11996e36a195e74aa3f13b22b32f31024d565580532703b3

&#x20;   txid #4             : 3c8de66e0d6ca8ef397f3f0a438783179f6d4124f5bce864b5bde6f12e56a009

&#x20;

\==========================================================================

\--- block #3, blocktime 2022-05-03 17:22:31 +0000 UTC:

&#x20;   total tx count      : 4

&#x20;

&#x20;  (type): Synthetic Anchor

&#x20;  Transaction Type: synthetic Anchor

&#x20;  Source: acc://bvn-BVN1

&#x20;  Major: false

&#x20;  RootAnchor: 49a1be0b0dc147d199c37e7c7e5cfd3107f1e437a6d82f32dc7fd6024e835289

&#x20;  RootIndex: 10

&#x20;  AcmeBurnt:

&#x20;     (type): Int

&#x20;  Block: 1

&#x20;  AcmeOraclePrice: 0

&#x20;  Receipts:

&#x20;

&#x20;  (type): Synthetic Anchor

&#x20;  Transaction Type: synthetic Anchor

&#x20;  Source: acc://bvn-BVN0

&#x20;  Major: false

&#x20;  RootAnchor: f5ec625566aebf3c0ef06883d836ef40bc91995ad0581491ee2d099d215ae7b4

&#x20;  RootIndex: 12

&#x20;  AcmeBurnt:

&#x20;     (type): Int

&#x20;  Block: 1

&#x20;  AcmeOraclePrice: 0

&#x20;  Receipts:

&#x20;

&#x20;

**Block Validator Network Minor Blocks**

&#x20;

accumulate blocks minor \[subnet-url] \[start index] \[count] \[tx fetch mode expand|ids|countOnly|omit (optional)] \[filter synth-anchors only blocks true|false (optional)] Get minor blocks

&#x20;

./accumulate blocks minor acc://bvn-bvn0 0 2

&#x20;

&#x20;       Minor block result Start: 0      Count: 2        Total: 0

\==========================================================================

\--- block #1, blocktime 2022-05-03 17:20:17 +0000 UTC:

&#x20;   total tx count      : 3

&#x20;   txid #1             : e43be90e349210456662d8b8bdc9cc9e5e46ccb07f2129e7b57a8195e5e916d5

&#x20;   txid #2             : c843452b4943c755c020ddc10b156fc78c712a187ce048f9036bda1703e03ef4

&#x20;   txid #3             : 0b6c57a48522f77d11996e36a195e74aa3f13b22b32f31024d565580532703b3

&#x20;

\==========================================================================

\--- block #3, blocktime 2022-05-03 17:22:31 +0000 UTC:

&#x20;   total tx count      : 3

&#x20;

&#x20;  (type): Synthetic Anchor

&#x20;  Transaction Type: synthetic Anchor

&#x20;  Source: acc://dn

&#x20;  Major: false

&#x20;  RootAnchor: e5d3857d3766c53dd2831b550e3ca05d87a15549befd678cd6e5ec338ba97474

&#x20;  RootIndex: 13

&#x20;  AcmeBurnt:

&#x20;     (type): Int

&#x20;  Block: 1

&#x20;  AcmeOraclePrice: 500

&#x20;  Receipts:

&#x20;

&#x20;  (type): Synthetic Anchor

&#x20;  Transaction Type: synthetic Anchor

&#x20;  Source: acc://dn

&#x20;  Major: false

&#x20;  RootAnchor: e5d3857d3766c53dd2831b550e3ca05d87a15549befd678cd6e5ec338ba97474

&#x20;  RootIndex: 13

&#x20;  AcmeBurnt:

&#x20;     (type): Int

&#x20;  Block: 1

&#x20;  AcmeOraclePrice: 500

&#x20;  Receipts:

&#x20;

&#x20;

&#x20;****&#x20;

&#x20;****&#x20;

&#x20;****&#x20;

&#x20;****&#x20;

&#x20;****&#x20;

&#x20;****&#x20;

&#x20;****&#x20;

&#x20;****&#x20;

&#x20;

&#x20;

&#x20;

&#x20;

&#x20;

&#x20;

&#x20;

&#x20;

***

&#x20;\[BS1]New get command will be able to query credits for lite token  \[BS1]

&#x20;\[BS2]This is will be removed \[BS2]

if the account url is a lite token account you do not have to specify the signing key \[BS3] \[BS3]

token issuer url \[BS4] \[BS4]

&#x20;\[BS5]Must add .0 at the end or it thinks it is a key page \[BS5]
