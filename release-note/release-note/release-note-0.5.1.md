# Release Note 0.5.1

### **Accumulate 0.5.1 -** April 30th 2022&#x20;

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
