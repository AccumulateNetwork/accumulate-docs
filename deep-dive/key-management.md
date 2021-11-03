---
description: An overview of Accumulate's hierarchical key structure
---

# Key Management

The Accumulate network is a collection of independent chains. Each chain is managed by a hierarchy of identities known as Accumulate Digital Identifiers (ADIs), and each identity possesses a hierarchy of keys that allow it to participate in the execution of transactions. &#x20;

Recall that a digital signature of a transaction is created by using the sender’s private key to encrypt a hash of the transaction output data to be unlocked. The receiver verifies the transaction by decrypting the digital signature with the sender’s public key and comparing the resulting hash to the hash of the transaction data. If the two hashes are identical, the transaction is considered valid because the public key used to decrypt the digital signature must correspond to the private key used to create it. This is commonly referred to as a single signature transaction. An illustration of the process used to create and validate a digital signature is shown below.

![An illustration of the process for creating a digital signature (left) and validating a digital signature (right)](<../.gitbook/assets/Digital signatures.png>)

A multisignature (multisig) transaction is similar except that _m_ of _n_ signatures are required to validate the transaction. For example, a withdrawal of funds from an account may be executed in a smart contract if 3 out of 4 account managers sign the transaction with their private keys.

The Accumulate protocol will allow single signature transactions in Testnet 1.0 and multisig in future Testnet releases. Its hierarchical key architecture will also enable key management through the use of keys with different priority levels. Multisig transactions and key management in the Accumulate protocol are illustrated in the example below, where a wallet that is owned by ADI RedWagon creates a token transaction, signs it with its private key, and submits it to a particular chain. The chain specifies what Key Book applies to the transaction, while the transaction specifies what Key Page must be used to validate it.&#x20;

![](<../.gitbook/assets/Accumulate Key Books.png>)

A Key Page defines the set of keys (_m_ of _n_) that are required to validate a transaction, where _m_ number of keys are created by hashing _m_ number of public keys. If validation requires a signature from any one key, then _m_ is equal to 1. If validation requires a signature from all keys, then _m_ is equal to _n_.&#x20;

A Key Book is a prioritized list of Key Pages where the first page in the list is the highest priority and the last page is the lowest priority. For example, the first key page can modify any key page, but the last key page can only modify itself.&#x20;

Each chain is attached to a Key Book, in the sense that the chain’s data record in the database specifies the chain ID of a Key Book, and each transaction has an actor (aka sponsor). When the protocol receives a transaction, the node loads the actor’s data record, locates the chain ID of the Key Book, and loads that particular Key Book. The transaction also specifies a Key Page priority, which is also an index. That index/priority refers to a Key Page within the key book that is associated with the actor. The keys in that Key Page are authorized to sign the transaction. If the transaction is signed by a key that is not in that Key Page, that signature is rejected.

In the example above, RedWagon/Account is governed by a Key Book belonging to RedWagon, and a transaction sent by RedWagon/Account specifies the priority 1 Key Page. This Key Page requires 4 keys out of 4 total keys (_m_ = _n_ = 4) to sign the transaction before it is valid.
