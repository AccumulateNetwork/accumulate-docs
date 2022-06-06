# Release Notes

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
