---
description: Easing the transition from Factom to Accumulate
---

# Factom API support

### **Introduction**

&#x20;Factom was originally deployed in 2015. Its API has been used on many projects and by many exchanges. This paper looks at the API as it exists and details what we can do to make the Accumulate API match to the extent possible. This paper outlines what we could do to bridge Factom to Accumulate. This will not be fully implemented by Activation, and we may not ever entirely implement the calls described in this document.&#x20;

### **Factom API**

The API is designed for outside applications to process transactions and interact with the Factom federated servers. The listening port can be configured and runs on 8088 by default. All these APIs use JSON-RPC, a remote procedure call protocol encoded in JSON. It is a very simple protocol (and very similar to XML-RPC), defining only a handful of data types and commands.&#x20;

They can be invoked in your terminal as:&#x20;

```
curl -X POST --data-binary '{"jsonrpc": "2.0", "id": 0, "method": "METHOD_HERE", "params": {"PARAM_1":"PARAM_DATA_1"}}' -H 'content-type:text/plain;' http://localhost:8088/v2 
```

The output will also be JSON.&#x20;

We will go through the Factom API as it exists today and detail what we believe we can provide on Accumulate.

### **Factom API to Accumulate API mappings**

[**ablock-by-height**](https://docs.factomprotocol.org/start/factom-api-docs/factomd-api#ablock-by-height) -- Not supported&#x20;

[**ack**](https://docs.factomprotocol.org/start/factom-api-docs/factomd-api#ack) -- Only requires the transaction hash, however.&#x20;

Returns Jason for entry and factoid transactions.&#x20;

Accumulate has no commit transactions, so ack cannot return them Accumulate does have entries, so ack can return the entry reveals Requires a transaction date and a block date for factoid transactions&#x20;

[**admin-block**](https://docs.factomprotocol.org/start/factom-api-docs/factomd-api#admin-block) -- Not supported&#x20;

[**chain-head**](https://docs.factomprotocol.org/start/factom-api-docs/factomd-api#chain-head) -- Returns the first entry of a given data account&#x20;

[**commit-entry** ](https://docs.factomprotocol.org/start/factom-api-docs/factomd-api#commit-entry)

Commit-entry creates the signature for signing an entry and puts it in the wallet database keyed by the entry hash. Nothing is submitted to Accumulate at this time.&#x20;

Reveal-entry creates the entry transaction and combines the entry transaction with the signature provided by commit-entry. The transaction is then submitted to Accumulate.



[**current-minute**](https://docs.factomprotocol.org/start/factom-api-docs/factomd-api#current-minute) --&#x20;

Returns&#x20;

* Leaderheight -- DVN height /600 (10 minute cadence)&#x20;
* DirectoryBlockHeight -- DVN height /600 (10 minute cadence)&#x20;
* Minute -- (DVN height / 60) % 10 (minutes within a 10 minute cadence)&#x20;
* Currentblockstarttime -- Timestamp of the first DVN minor block in a 10 minute cadence
* Currentminutestarttime -- First DVN minor block of the current minute in a 10 minute cadence
* Directoryblockinseconds -- 600&#x20;
* Stalldetected -- returns true if Accumulate detects a stall of the node&#x20;
* Faulttimeout -- returns 0&#x20;
* Roundtimeout -- returns 0&#x20;
* [**dblock-by-height**](https://docs.factomprotocol.org/start/factom-api-docs/factomd-api#dblock-by-height) -- Not supported&#x20;
* [**directory-block**](https://docs.factomprotocol.org/start/factom-api-docs/factomd-api#directory-block) -- Not supported&#x20;
* [**directory-block-head**](https://docs.factomprotocol.org/start/factom-api-docs/factomd-api#directory-block-head) -- Not supported&#x20;
* [**ecblock-by-height**](https://docs.factomprotocol.org/start/factom-api-docs/factomd-api#ecblock-by-height) -- Not supported&#x20;
* [**Entry**](https://docs.factomprotocol.org/start/factom-api-docs/factomd-api#entry) -- Given an entry hash, return the entry in JSON form&#x20;
* [**Entry-ack**](https://docs.factomprotocol.org/start/factom-api-docs/factomd-api#entry-ack) -- Deprecated; not supported&#x20;
* [**Entry-block**](https://docs.factomprotocol.org/start/factom-api-docs/factomd-api#entry-block) -- Not supported&#x20;
* [**Entry-credit-balance** ](https://docs.factomprotocol.org/start/factom-api-docs/factomd-api#entry-credit-balance)-- The address specified must be a url to a key page. Returns the credit balance&#x20;
* [**Entrycredit-block**](https://docs.factomprotocol.org/start/factom-api-docs/factomd-api#entrycredit-block) -- Not supported.

{% hint style="info" %}
Note that minute times are approximate.  Even in Factom, minute times could stretch or compress depending upon how the various leaders synced, or if a leader had to be replaced.
{% endhint %}

* [**Entry-credit-rate**](https://docs.factomprotocol.org/start/factom-api-docs/factomd-api#entry-credit-rate) -- Returns the price of credit in ACME (fixed point)
* [**Factoid-ack**](https://docs.factomprotocol.org/start/factom-api-docs/factomd-api#factoid-ack) -- Deprecated; not supported
* [**Factoid-balance**](https://docs.factomprotocol.org/start/factom-api-docs/factomd-api#factoid-balance) -- Returns the number of ACME at a given Lite Data Account (which can be specified with the FA address).  If a URL is provided instead of an address, factoid-balance can return the number of ACME at an ADI Token Account.
* [**Factoid-block**](https://docs.factomprotocol.org/start/factom-api-docs/factomd-api#factoid-block) -- Not Supported
* [**Factoid-submit**](https://docs.factomprotocol.org/start/factom-api-docs/factomd-api#factoid-submit) -- Submit a binary transaction as long as it is properly encoded and signed to Accumulate.
* [**Fblock-by-height**](https://docs.factomprotocol.org/start/factom-api-docs/factomd-api#fblock-by-height) Not Supported
* [**Heights**](https://docs.factomprotocol.org/start/factom-api-docs/factomd-api#heights) -- Returns the last confirmed Directory Validator Block for all heights
* [**Multiple-ec-balances**](https://docs.factomprotocol.org/start/factom-api-docs/factomd-api#multiple-ec-balances) -- all addresses must be key page urls. The call is broken up into individual calls for each key page url.  `Currentheight` and `lastsavedheight` are both the current height of the DVN
* [**Multiple-fct-balances**](https://docs.factomprotocol.org/start/factom-api-docs/factomd-api#multiple-fct-balances) -- all addresses must be token account urls.  The call is broken up into individual calls for each token account.  `Currentheight` and `lastsavedheight` are both the current height of the DVN
* [**Pending-entries**](https://docs.factomprotocol.org/start/factom-api-docs/factomd-api#pending-entries) -- returns `0`.  Accumulate does not have the commit/reveal exchange with applications and users, so writes do not pend like they do in Factom
* [**Pending-transactions**](https://docs.factomprotocol.org/start/factom-api-docs/factomd-api#pending-transactions) -- return any pending transactions in the signature chain for a particular transaction account.  No changes to the JSON format are required.  The “fees” entry on each transaction will be `0`.  (This is because Accumulate does not require the inputs to be more than the outputs to pay fees but rather uses credits on the signing key page to pay fees.)
* [**Properties**](https://docs.factomprotocol.org/start/factom-api-docs/factomd-api#properties) -- will return&#x20;

```
{ "jsonrpc": "2.0", "id": 0, "result": { "factomdversion": "0.5.0.0", "factomdapiversion": "3.0" } }
```

* [**Raw-data**](https://docs.factomprotocol.org/start/factom-api-docs/factomd-api#raw-data) -- Retrieve an entry or transaction in raw format.  Data is a hex encoded string.
* [**Receipt**](https://docs.factomprotocol.org/start/factom-api-docs/factomd-api#receipt) -- Retrieve a receipt for a transaction hash or entry hash.  This will be in Accumulate format
* [**Reveal-chain**](https://docs.factomprotocol.org/start/factom-api-docs/factomd-api#reveal-chain)

Reveal-chain is implemented as a Reveal-entry but creates a new Lite Data Account as well. This may be difficult to implement without a new call to create the Lite Data Account

* [**Reveal-entry**](https://docs.factomprotocol.org/start/factom-api-docs/factomd-api#reveal-entry)&#x20;

Commit-entry creates the signature for signing an entry and puts it in the wallet database keyed by the entry hash. Nothing is submitted to Accumulate at this time. Reveal-entry creates the entry transaction and combines the entry transaction with the signature provided by commit-entry. The transaction is then submitted to Accumulate.

* [**Send-raw**](https://docs.factomprotocol.org/start/factom-api-docs/factomd-api#send-raw-message) -- Supported&#x20;

Sending a raw transaction allows transactions to be created off-line in secure environments and submitted to the network on a “hot” platform. Also useful for testing and debugging. Any transaction created for the Accumulate protocol should be available in raw form for disconnected construction.

[**Transaction**](https://docs.factomprotocol.org/start/factom-api-docs/factomd-api#transaction) -- Supported&#x20;

Caveats include:&#x20;

* No transaction block,&#x20;
* directory block can be reported Directoryblockheight will be reported as the DNV minor block height / 600

### **Factom Wallet API**&#x20;

* [**Add-ec-output**](https://docs.factomprotocol.org/start/factom-api-docs/factom-walletd-api#add-ec-output) -- Not supported
* [**Add-fee**](https://docs.factomprotocol.org/start/factom-api-docs/factom-walletd-api#add-fee) Noop: we do not charge fees in the same way Factom did)
* [**Add-input**](https://docs.factomprotocol.org/start/factom-api-docs/factom-walletd-api#add-input) Only allow the addition of one input
* [**Add-output**](https://docs.factomprotocol.org/start/factom-api-docs/factom-walletd-api#add-output) Supported
* [**Address**](https://docs.factomprotocol.org/start/factom-api-docs/factom-walletd-api#address) Creates a lite token account address
* [**All-addresses**](https://docs.factomprotocol.org/start/factom-api-docs/factom-walletd-api#all-addresses) Returns all the key books and token accounts managed by the wallet
* [**Compose-chain**](https://docs.factomprotocol.org/start/factom-api-docs/factom-walletd-api#compose-chain) -- Not supported
* [**Compose-entry** ](https://docs.factomprotocol.org/start/factom-api-docs/factom-walletd-api#compose-entry)-- Not supported
* [**Compose-transaction**](https://docs.factomprotocol.org/start/factom-api-docs/factom-walletd-api#compose-transaction) Marshals the current transaction into a hex encoded string. Compose-transaction fails if the current transaction is incomplete and/or has not been signed.  Returns a hex string that can be inputted into the factomd API [factoid-submit](https://docs.factomprotocol.org/start/factom-api-docs/factomd-api#factoid-submit) to be sent to the network.
* [**Delete-transaction**](https://docs.factomprotocol.org/start/factom-api-docs/factom-walletd-api#delete-transaction) Delete the current transaction under constructed
* [**Generate-ec-address**](https://docs.factomprotocol.org/start/factom-api-docs/factom-walletd-api#generate-ec-address) -- Not Supported
* [**Generate-factoid-address**](https://docs.factomprotocol.org/start/factom-api-docs/factom-walletd-api#generate-factoid-address) Create a lite token account address
* [**Get-height**](https://docs.factomprotocol.org/start/factom-api-docs/factom-walletd-api#get-height) -- Not supported
* [**Import-addresses**](https://docs.factomprotocol.org/start/factom-api-docs/factom-walletd-api#import-addresses) Import Factoid address secret keys into the wallet
* [**Import-koinify**](https://docs.factomprotocol.org/start/factom-api-docs/factom-walletd-api#import-koninify) Import a Koinify crowd sale address into the wallet.
* [**New-transaction**](https://docs.factomprotocol.org/start/factom-api-docs/factom-walletd-api#new-transaction) Create a new transaction to be built using other calls
* [**Properties**](https://docs.factomprotocol.org/start/factom-api-docs/factom-walletd-api#properties) Retrieve current properties of the factom-walletd, including the wallet and wallet API versions
* [**Sign-transaction**](http://sign-transaction) Signs the transaction under construction
* [**Sub-fee**](https://docs.factomprotocol.org/start/factom-api-docs/factom-walletd-api#sub-fee) Noop. it does nothing because we do not pay fees on Accumulate by a difference between inputs and outputs
* [**Tmp-transactions**](https://docs.factomprotocol.org/start/factom-api-docs/factom-walletd-api#tmp-transactions) Lists all current working transactions in the wallet.  None of these transactions have been sent
* [**Transactions (Retrieving)**](https://docs.factomprotocol.org/start/factom-api-docs/factom-walletd-api#transactions-retrieving) Return transactions using a range, by TxID, by Address.  All Transactions are not supported
* [**Wallet-backup**](https://docs.factomprotocol.org/start/factom-api-docs/factom-walletd-api#wallet-backup) Return the wallet seed and all addresses in the wallet for backup and offline storage
* [**Wallet-balances**](https://docs.factomprotocol.org/start/factom-api-docs/factom-walletd-api#wallet-balances) Return balances of all addresses in the wallet
