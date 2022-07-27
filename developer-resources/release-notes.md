# Release Notes

**Accumulate v1.0** **and Release Candidate1 (RC1) Release Notes – 07/19/22**&#x20;

**🚀  New** &#x20;

* Add network file deployment test&#x20;
* \`.acme\` is a valid ADI name&#x20;
* A synthetic transaction will never be delivered if it arrives after its anchor**.**&#x20;
* Add Entry Blocks to the flat files of the Factom Entry Extraction&#x20;
* Add guards for –reset&#x20;
* Add security for proxy / validator config&#x20;
* Allow new Factom data entries&#x20;
* Block self-delegation&#x20;
* CLI import key makes bad assumption about key type&#x20;
* CLI tx execute: accept YAML&#x20;
* Configurable routing&#x20;
* Convert batch to data model entity&#x20;
* Convert transaction to data model entity&#x20;
* Create data model based database infrastructure&#x20;
* Create Snapshot of Factom Entries&#x20;
* Dataset logger for creating tabular data&#x20;
* Debug TestMissingSynthTxn&#x20;
* Deprecate use of persistent peers&#x20;
* Enforce anchor sequence and delivery&#x20;
* Gen-types –include is broken&#x20;
* Halt Factom at a Particular Block Height&#x20;
* Include a version in the snapshot header&#x20;
* Include the list of accounts within an ADI as part of the ADI’s state&#x20;
* Leverage checktx priority for SyntheticTransactions&#x20;
* Lock lite token accounts&#x20;
* Major Block API Task&#x20;
* Make transaction blacklist marshal as a list&#x20;
* Make validator key books subordinate to dn/operators&#x20;
* Minor block API excludes anchors&#x20;
* Move account indices to data model&#x20;
* Multiple output issue tokens&#x20;
* Not able to generate lite Identity/lite token account with already created “key”/”public key”&#x20;
* Partially Refund ACME Balance for Failed Add Credit Transaction (Deduct 1 Credits worth of ACME)&#x20;
* Preserve state during CheckTx&#x20;
* Prevent refund cycle&#x20;
* Reduce the signature fee to match the scratch write data fee&#x20;
* Refactor accumulated config directory structure&#x20;
* Refactor transaction status&#x20;
* Remove grpc support &#x20;
* Remove IDE-specific files&#x20;
* Remove Private Key import from command line input in CLI&#x20;
* Remove the validator key book&#x20;
* Replace scratch accounts with scratch chains&#x20;
* TestAdd/RemoveKey tests broken&#x20;
* Update indices and SMT to use the struct cache&#x20;
* Update the Devnet to run in dual-mode (pairing BVN node and DN node)&#x20;
* Update type generator&#x20;
* UpdateKey can create duplicates&#x20;
* Use a fixed set of chains&#x20;
* Use a full snapshot as the genesis document&#x20;
* Use data model for database cache&#x20;
* Use full chainId/accountId as the lite data url&#x20;
* Validate major block API in CI and make major block timing configurable&#x20;
* Validate synthetic and anchor signers against dn/network&#x20;
* Wallet Backup Import and Export Design&#x20;
* When Creating a Duplicate Authority the Transaction Should Fail&#x20;
* Write Load Code Utility&#x20;

🔧 **Fixes**&#x20;

* Able to Set Threshold to 0&#x20;
* Fix add credits&#x20;
* Handle IssueTokens failure&#x20;
* Issuing Custom Tokens to an ACME Token Account Changes ACME Account Balance&#x20;
* Not able to generate lite Identity/lite token account with already created “key”/”public key”&#x20;
* Panic in SubnetSyntheticLedger.Add&#x20;
* Sending a synthetic transaction to the DN crashes it&#x20;
* TestCLI is failing in CI (June 13)&#x20;
* Updating a Key Book URL and Public Key Hash with a different Delegate (Key Book URL) (signing with the Public Key Hash)(Entry: Public Key Hash, Delegate) Fails&#x20;
* Updating a Public Key Hash Entry to Include the Same Public Key and a New Key Book URL Produces a “Cannot have duplicate entries on key page” Error&#x20;

**✨** **Improvements** &#x20;

* Cleanup CLI help&#x20;
* Fix static analysis issues&#x20;
* Many CLI subcommands appear to accept more parameters than they really do&#x20;
* Remove key page index and height parameters from CLI commands&#x20;
* Rename subnet to partition&#x20;

****

**Accumulate 0.6.1 Release Notes – 06/02/22**

**🚀  New**&#x20;

* Routing debug tool
* Remove redundant slippage parameter from CLI credit purchase
* Handle synthetic transactions sent out of order
* Rename key page entry ‘owner’ to ‘delegate’
* Eliminate the mirror transaction
* Add linters
* Sign a message with the cli
* Anchor the DN in the DN
* Require approval from a key book when adding that key book to the authority set of an account
* Review Rosetta API Endpoints
* Staking Implementation Document
* Eliminate the data chain
* Split up synthetic anchor transaction
* Query specific block by height
* Create the operator key books
* Major block design
* Clarify wording in receipt
* Add test coverage for legacyEd25519, btc, btcLegacy, eth in CLI tests
* ABCI snapshot functions
* Do not create empty blocks
* Require proof of external dependencies when executing certain operations
* Guarantee synthetic transaction delivery

🔧  **Fixes**&#x20;

* [AC-1525](https://accumulate.atlassian.net/browse/AC-1525) Improve error messages
* Fix flaky anchor test
* API does not support delegated signatures
* Query-minor-blocks does not return “total”
* Refactor delegated signatures and key handling
* Unionize executor requests
* Make data entry a tagged union
* Move test coverage of administrative test function in validate.sh to separate file

### ****

### **Accumulate 0.5.1 -** April 30th 2022 ****&#x20;

🚀  **New**&#x20;

* We have added support for executing multiple key page updates as a single transaction (We have added a multi-operation key page updates)&#x20;
* We added API support for other signature types&#x20;
* Create an access control framework&#x20;
* Add transactions for adding, removing, updating a validator&#x20;
* Envelope and synthetic transaction redesign&#x20;
* Capture evidence from Tendermint&#x20;
* Capture votes from Tendermint&#x20;
* Create index chains&#x20;
* Add an API call that constructs a proof of the state of an account&#x20;
* Add memo and metadata field to the transaction&#x20;
* CLI Command to display how many Credits you receive per ACME&#x20;
* Add the ability to lock a key page&#x20;
* Support Factom RCD1 signatures&#x20;
* We created Sub-ADIs&#x20;

&#x20;

🔧  **Fixes**&#x20;

* A synthetic transaction with an invalid origin is not saved&#x20;
* We fixed a bug that could cause the TestNet to stall due to an invalid synthetic transaction We built a solid Monitoring infrastructure&#x20;

&#x20;

🔧 **Improvements**&#x20;

* Key page entries must be key hashes&#x20;
* Deprecate extids on data accounts&#x20;
* Document API methods&#x20;
* Rename the pending chain&#x20;
* Run two nodes side-by-side&#x20;
* Use 'timestamps' instead of 'nonces'&#x20;
* Track the key page version&#x20;
* Track issued tokens instead of remaining reserve&#x20;
* Accumulate only check the nonce of the first signature&#x20;
* Burn ACME to buy credits&#x20;
* We added Nest Key Pages with Key Books (acc://ethan/book/1)&#x20;
* Keys must be hashed with SHA-256&#x20;

&#x20;

&#x20;

### **Accumulate - Version 0.5**  February 1st 2022

&#x20;

**🚀  New**&#x20;

* &#x20;Expose the number of signatures required for a pending transaction in the protocol&#x20;
* &#x20;Assign a manager to an account in the CLI&#x20;
* &#x20;Lite Account Identity in the CLI&#x20;
* Add Scratch Flag to ADI Data Account and ADI Token Account Creation in CLI&#x20;
* Add Token Issuance to CLI&#x20;
* Prove the inclusion of an entry in a chain&#x20;
* Support signatures other than ED25519 in the protocol&#x20;

&#x20;

**🔧  Fixes**&#x20;

* Add human-readable output for token transactions in the CLI&#x20;
* URL-based query for a data entry by hash returns the wrong entry hash in the protocol&#x20;
* CLI can't read Account Balance&#x20;

&#x20;

🔧 **Improvements**&#x20;

* Improved the Update key book references in the protocol&#x20;
* Allow the version check to be ignored when onboarding a node in the CLI&#x20;
* Create a CLI Command to Un-assign a Manager&#x20;
* Improved Document new encoding scheme in the protocol&#x20;
* Improved manual ACME oracle in the protocol&#x20;
* Improved the return Threshold of Pending Transaction Through API in the protocol&#x20;
* SDK Backwards compatibility for token issuer&#x20;
* Use the SDK client interface improved&#x20;
* Change Token Type for Token Issuer &#x20;
* Display Synthetic Transaction Success or Failure in CLI &#x20;
* Add Command to CLI to show Pending TXs&#x20;
* Make a chain unmanaged&#x20;
* Add a manager to an existing chain&#x20;
* Assign manager key book when a record is created&#x20;
