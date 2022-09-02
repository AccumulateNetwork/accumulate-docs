# Release Note 0.5

### **Accumulate - Version 0.5**  February 1st, 2022

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
