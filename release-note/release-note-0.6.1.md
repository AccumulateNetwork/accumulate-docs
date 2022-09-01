# Release note 0.6.1



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
