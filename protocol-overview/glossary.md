---
description: A list of Accumulate-centric terminology and definitions
---

# Glossary

#### Accumulate Digital Identifier (ADI)

An ADI is an account that can hold sub-accounts under itself. These sub-accounts are different chains that store information on the Accumulate Network. An ADI can manage multiple types of chains i.e. Token Account Chain, Data Chain, Scratch Chain, Token Issuance Chain, Key Chain, Managed Chains. The ADI name can be customized based on the preferences of the user.

#### Accumulate Network

The Accumulate network is a collection of independent chains. Each chain is managed by a hierarchy of identities known as Accumulate Digital Identifiers (ADIs), and each identity possesses a hierarchy of keys, which allows it to participate in the execution of transactions.

#### ADI Data Account

An ADI can contain a data account. We call this an ADI data account. The ADI Data Account is a layer that allows ADI accounts to add and organize data to the blockchain

#### ADI Token Account

ADI Token Accounts hold tokens. ADI Token Accounts can send tokens to other Lite Accounts or ADI Token Accounts.

#### Admin Keys

Admin Keys are used to make changes to keys and key types, which are used to manage an identity. Admin keys have priorities. The highest priorities can be kept in cold storage, while the lower priority keys are in active use to maintain an Identity. Admin keys can be replaced or retired with any sort of key signature as needed to manage the identity.

#### Anchor Chain

A chain that aggregates anchors from other chains (transactions, merkle tree & BVNs) capturing the states of the network.

#### Block Validator Network

A tendermint network of nodes that execute transactions against records. BVNs act as independent blockchains that build blocks for parts of the Accumulate blockchain. BVNs serve as their own roots of possible nodes, breaking up the job of validating transactions. BVN Sub-chains hold Merkle roots of chains collected and managed by a BVN. Effectively allows the sharding of BVN nodes, which in turn shard Accumulate.

#### Credits

Credits are a non-transferable form of payment on the Accumulate Network. Credits are created by converting ACME tokens into credits. Once the user converts ACME tokens to purchase credits, credits are then used for actions on the network such as the creation of an ADI, ADI Token Account, or Updating Keys in a Key Page.

#### Data Keys

Data Keys authorize data writes to data chains. Data Keys can be restricted to particular data chains.

#### Directory Network (DN)

BVNs are tied together by a blockchain called the Directory Network (DN), which builds directory blocks for Accumulate. The DN collects the summary hash for all the BVNs and puts them in a directory block for every block period. The DN acts as a directory service for Accumulate and resolves questions about the state of Accumulate at every block.

#### Keybook

A Keybook maintains a set of keypages ordered by priority.

#### Keypage

A Key Page holds a list of the hash of public keys and determines signature specifications (single-sig, multi-sig).

#### Keys

Keys are signatures that are required for submitting transactions.

#### Lite Account

Lite Accounts are accounts that are not tied to Identity, however, they can send transactions using ACME. Lite Accounts can send transactions to other Lite Accounts or ADI Token Accounts. Lite Accounts are URL-based, but those addresses feature a series of hexadecimal characters.

#### sub-ADI

An ADI can contain another ADI. We call this a sub-ADI. While an ADI contains accounts, a sub-ADI contains sub-accounts.

#### Synthetic Transactions

Synthetic Transactions are transactions that are submitted by the protocol rather than by the user. This allows the BVN hosting the user to completely process the transaction on its own, and allows it to notify the remaining BVNs of the transaction after it has been completed. Since the BVN that processed the transaction does not have to wait on the others, this allows for faster processing times of transactions.

#### Token Keys

Token Keys authorize token transactions. They can be restricted to particular tokens.
