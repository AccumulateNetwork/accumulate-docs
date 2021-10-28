---
description: How to create Accumulate Digital Identifiers (ADIs)
---

# Accumulate Digital Identifiers

**1.  Introduction**

All operations on the Accumulate network are managed by an enhanced version of Distributed Digital Identities and Identifiers (DDIIs) that we refer to as Accumulate Digital Identifiers (ADIs). ADIs can send and receive tokens like a Bitcoin address, issue smart contracts like an Ethereum address, and facilitate a variety of new and complex operations such as consensus building and key management. Each ADI operates as its own independent chain under which all the states for a user’s identity including its keys, data, token accounts, and sub-identities can be managed on the network. The ability to automate operations and enable multisignature (multisig) authorization gives ADIs the flexibility to be managed by an individual, an organization, or even a device (e.g. IoT sensors). ADIs can also be transferred or controlled by multiple parties to create a consortium that manages a user’s identity and data.

In this technical document, we will discuss the identity ecosystem, the construction of ADIs, and the implementation of data, token, and identity chains on the Accumulate network. For an introduction to ADIs and the identity framework of Accumulate, please refer to the Litepaper. For a discussion of identity use cases, please refer to ADI Use Cases.



**2.  The Identity Ecosystem**

**2.1.  Names**

Websites are UTF-8 encoded and addressed by URLs, with domains indicating the owner and directory paths specifying the various pages that are associated with the domain. ADIs are also UTF-8 encoded and URL indexable, but with domains specifying the name of an ADI and subdomains specifying the associated subchains (e.g. data, transactions, and sub-identities). This design allows international human readable names to be used as identifiers, and enables integration with browsers and enterprise tech stacks. An example of an ADI URL for an identity with the name “RedWagon” would be:

_acc://RedWagon_

If ADI RedWagon contained a token chain named “AcmeTokens”, the chain URL would simply b

_acc://RedWagon/AcmeTokens_

Compare the addressing format of ADIs with that of other blockchains and note that any number of sub-chains can be indexed under the same ADI:

|            |                                                  |
| ---------- | ------------------------------------------------ |
| Accumulate | acc://RedWagon                                   |
| Bitcoin    | bc1qd9qdr257xpultejescdf72y4n005y39b43dnqn       |
| Litecoin   | M8T1B2Z97gVdvmfkQcAtYbEepune1tzGua               |
| Ethereum   | 0xe2e3880095d133d341400b2b35c0195c7154ccfb       |
| Polkadot   | 14Y4s6V1PWrwBLvxW47gcYgZCGTYekmmzvFsK1kiqNH2d84t |
| Cosmos     | cosmos1t5u0jfg3ljsjrh2m9e47d4ny2hea7eehxrzdgd    |
| Solana     | 9JcnETeXxJSsVtJYhWSih8HinDYk7bPLSmziYKYC3yZ6     |



A large corporation might create a sub-chain for each department and additional sub-chains for groups and managers. Identities are hierarchical, so a department would be under the control of the company’s ADI just as a group would be under the control of a department. However, a company could also create multiple independent ADIs, each with the authority to create and manage any number of sub-identities. An identity chain may be organized like the following:

_acc://Company.com/_

_acc://Company.com/i/Accounting/_

_acc://Company.com/i/Accounting/i/Payroll_

Designations such as “i” for different identities under the management of an ADI may be inserted by applications for context, but are not necessary on the protocol.

**2.2.  Tokens**

Tokens are referenced by URLs and handled in their own sub-chains, which enables a user to send and receive tokens through their identity. The destination ADI, token identity, and quantity are required to transfer tokens between ADIs as in the following example:

_Send ( token, dest, amount)_

_Send ( BTC, Alice, .0125)_

Here, 0.0125 BTC are transferred to ADI Alice from an external ADI. The Accumulate network has a registry of common tokens (e.g. BTC, ETH, SOL) that are referenced by URL and handled in their own sub-chains under the management of an ADI. In the example below, user Bob has created a directory “t” to refer to tokens like BTC.

_acc://Bob/t/BTC_

It is also possible for an ADI to reference an unregistered token by URL or even issue its own tokens. This is typically done within an ADI to reduce state in the Accumulate network. However, any ADI can hold tokens that are registered by any other ADI by referencing the issuing ADI’s token registration in a token transaction. For example, Alice could issue 100 WhiteRabbit tokens and send 10 of them to Bob using the following command:

_CreateTokens Alice/t/WhiteRabbit 100_

_SendToken Alice/t/WhiteRabbit Bob/t/WhiteRabbit 10_

**2.3.  Keys**

In most blockchains, an address is the hash of a public key, and changes to a public key necessarily require a change of address. Moving private keys to new wallets and signing transactions to move assets exposes the asset holder to security risks. Audits of the blockchain may also flag such activity as a tax event. Accumulate addresses these problems by introducing a hierarchy of keys under the control of an ADI that can be added, deleted, rotated, or organized by priority level. Keys can be managed like signers to an account so new ADIs don’t need to be issued when a company shifts its responsibilities over time. This allows companies to upgrade or downgrade their security as needed, and use higher priority keys to grant or revoke access to lower priority keys. Keys are considered a sub-chain of an ADI, and can be categorized as administrative (admin) keys, token keys, and data keys.

**Admin Keys **have priority levels. High priority keys may be kept in cold storage, while low priority keys may be in active use to handle daily activities with low security requirements. Admin keys can be replaced or retired with a valid key signature.

**Token Keys **authorize token transactions. They may be restricted to particular tokens or authorized to issue tokens.

**Data keys **manage the organization of data. Large or complicated data sets may be indexed and hashed to categorize data and minimize its footprint.

Admin keys are defined by their Key Signatures and Key Records. Key Signatures may be public/private keys, multisig, or other identities in the network. Public/private keys use the Ed25519 digital signature algorithm, which allows for fast single-signature verification. The Key Record consists of the signature hash and priority level. The priority level is defined as an integer from 0 to N, where 0 specifies the highest priority key. Higher priority keys are authorized to make changes to lower priority keys within the user’s ADI or within another ADI as part of a multisig operation. However, each priority level can only map to one key. Adding a key with the same priority level replaces any existing key at that level.



**3.  Building an ADI**

**3.1.  General Overview**

An ADI is created after a sponsor initiates an “adi-create” transaction on the network. The sponsor can be an organization or a user so long as they spend the required amount of tokens. The validator on the sponsor’s identity chain will validate the adi-create transaction, create a synthetic transaction (those created by the protocol), and push that out to the network to be processed in the next block. The network where the new identity resides will receive the synthetic transaction from the Block Validator Chain (BVC) and validate it against the current state of the network. A successful identity creation requires 1) that signatures for the synthetic transaction must be valid and verified against the Directory Chain (DC) receipt and 2) that the identity does not already exist on the network. If the above criteria are met, an identity state object is created as illustrated in Figure 1. For an introduction to BVCs and DCs, please refer to the Litepaper. Synthetic transactions will be covered in more detail in future technical documents

![](<../.gitbook/assets/ADI illustration2.svg>)

**3.2.  Routing an ADI**

The Accumulate network uses URLs to reference user sub-chains that are managed by an ADI. The URL consists of the following characteristics

_acc://{ADI}/{ChainPath}_

where ADI refers to the user’s identity on the Accumulate network and ChainPath refers to ADI sub-chains. More accurately, the ADI is a Root Identity that is used to route transactions to Block Validators. Each chain within a Root Identity is handled by a particular Block Validator that is determined after deriving the SHA256 hash of the ADI and hashing this a second time (below) to create an address:

_AdiChainId =sha256( lowerCase(ADI) )_

Both the chain and sub-chain identity can be hashed such that the URL acc://RedWagon/AcmeTokens will be internally represented by the following:

_sha256( redwagon )_

_sha256( redwagon/AcmeTokens )_

ADIs are evenly distributed among BVCs, similar to how social media platforms evenly distribute large datasets to their servers. Network routing is determined by taking the first low-order eight bytes of the SHA256 hash of the ADI’s chain ID. The address corresponding to a particular Block Validator network is determined by the following:

_Address =uint64( sha256( AdiChainId ) \[0:8]) & UserMask_

_UserMask =0x7FFFFFFFFFFFFFFF_

where unint64 refers to the unsigned 64 bit end, which is 8 bytes long and specifies that all bits are positive. UserMask is the maximum 64-bit integer in hexadecimal that clears the high order bit. The end result is a random address that can be processed internally and distributed to Block Validator networks.



**4.  Identity Architecture**

The diagram below considers a multisig transaction that is managed by multiple identity chains to illustrate the concepts discussed above. Each identity has a master, or administrative key set and two sub-chains (Signature Groups A-F) that may specify names, tokens, or data. Each sub-chain has several Signature (Sig) Root Hashes that represent the Merkle root of a set of Key Records.

Group B of Identity A is the signer for the Main Chain. However, a transaction processed on the Main Chain will only be validated if Identities B and C can provide signatures that validate “n” number of “m” keys. In the example below, two out of four keys are required to reach a consensus. Identity A initiates the transaction, Identities B and C sign through Signature Groups C and E, and their signatures are stored in the Sig Record. Each signature is validated as it is received and stored on a Pending Chain until a consensus is reached or the transaction is terminated. If the transaction is approved, it will be validated on the Main Chain and processed on the Accumulate network in the next block.

Identities and keys can be managed over time such that the sudden departure of Identity B and the loss of the signature provided by Signature Group D does not have to break the consensus. Identity A, which is the signer for the Main Chain, can assign a new identity to fill the role of Identity B. It can also upgrade or downgrade security as needed. For example, Identity A could require an additional signature for consensus by creating a new identity or giving authority to an existing Signature Group in Identity B or C.

&#x20;

![](<../.gitbook/assets/ADI illustration new.svg>)

&#x20;
