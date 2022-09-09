# Release Note 1.0 RC1

**Accumulate v1.0** **and Release Candidate1 (RC1) Release Notes – 07/22/22**&#x20;

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
