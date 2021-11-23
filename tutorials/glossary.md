# Glossary

### Accumulate Network

The Accumulate network is a collection of independent chains. Each chain is managed by a hierarchy of identities known as Accumulate Digital Identifiers (ADIs), and each identity possesses a hierarchy of keys that allow it to participate in the execution of transactions.

### Accumulate Digital Identifier (ADI)

ADIs are URL-based digital identities with hierarchical key sets that can manage data, tokens, and sub-identities. Each ADI operates as its own independent chain under which all the states for a user’s identity including its keys, data, token accounts, and sub-identities can be managed on the network.
ADIs can send and receive tokens like a Bitcoin address, issue smart contracts like an Ethereum address, and facilitate a variety of new and complex operations such as consensus building and key management.

### ADI Token Account

An ADI can contain a token account. We call this an ADI token account.

### ADI Data Account

An ADI can contain data account. We call this an ADI data account.

### sub-ADI

An ADI can contain another ADI. We call this a sub-ADI. They can be considered as a type of identity sub-chains.

### Lite Account

A Lite Account consists of an identity and token URL. Lite Accounts are a ‘lite’ version of ADIs that can be used to send and receive tokens. 
Lite Accounts are automatically created by the network once a transaction is sent from an external wallet. Two Lite Accounts can interact with each other through deposits and withdrawals just as users can interact through traditional blockchain addresses. Lite Accounts also fulfill several important roles, including ADI sponsorship.

### Token Account

A token sub-chain is classified as Token Account.

### Data Account

A data sub-chain is classified as Data Account.

### Keys

Each identity of an ADI hierarchy, possesses a hierarchy of keys that allow it to participate in the execution of transactions. Keys are considered a sub-chain of an ADI, and can be categorized as administrative (admin) keys, token keys, and data keys.

### Keypage

A Key Page defines the set of keys that are required to validate a transaction. 

### Keybook

A Key Book is a prioritized list of Key Pages, where the first page in the list is the highest priority and the last page is the lowest priority. 

### Block Validator Network (BVN)

A tendermint network of nodes that execute transactions against records.

### BVN Anchor Chain

A chain that aggregates record anchors.

### Directory Network (DN)

a tendermint network of nodes that aggregates BVN anchors.

### DN Anchor Chain

A chain that aggregates BVN anchors
