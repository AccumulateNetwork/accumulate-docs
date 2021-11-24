# Glossary

### Accumulate Network

The Accumulate network is a collection of independent chains. Each chain is managed by a hierarchy of identities known as Accumulate Digital Identifiers (ADIs), and each identity possesses a hierarchy of keys that allow it to participate in the execution of transactions.

### Accumulate Digital Identifier (ADI)

An ADI is the umbrella account which holds sub accounts. These sub accounts are different chains that store information on the Accumulate Network. An ADI can have different chains that it manages i.e. Token Account Chain, Data Chain, Scratch Chain, Token Issuance Chain, Key Chain, Managed Chains.

### ADI Token Account

Tokens are held by identities in an ADI Token Account and can be sent to identities or Lite Accounts. ADI Token Accounts can send transactions to other Lite Accounts or ADI Token Accounts.

### ADI Data Account

An ADI can contain data account. We call this an ADI data account.

### sub-ADI

An ADI can contain another ADI. We call this a sub-ADI. They can be considered as a type of identity sub-chains.

### Lite Account

Accounts that are not tied to an Identity but can send transactions using ACME. Lite Accounts that can send transactions to other Lite Accounts or ADI Token Accounts. Lite Accounts are URL based but have a series of hexadecimal characters.

### Keypage

A Key Page holds a list of the hash of public keys and determines signature specifications (single-sig, multi-sig).

### Keybook

A Key Book maintains a set of key pages order by priority.

### Keys

Keys are signatures that are required for transaction.

### Admin Keys

Admin Keys are used to make changes to keys and key types that are used to manage an identity. Admin keys have priorities. The highest priorities can be kept in cold storage, while the lower priority keys are in active use to maintain an Identity. Admin keys can be replaced or retired with any sort of key signature as needed to manage the identity.

### Token Keys

Token Keys authorize token transactions. They can be restricted to particular tokens.

### Data Keys

Data Keys authorize data writes to data chains. They can be restricted to particular data chains.

### Credits

Credits are a non-transferable form of payment on the Accumulate Network. As user converts ACME tokens to purchase credits. Credits are then used for actions on the network such as the creation of an ADI, ADI Token Account, or Updating Keys in a Key Page.

### Block Validator Network (BVN)

A tendermint network of nodes that execute transactions against records. BVNs act as independent blockchains that build blocks for parts of the Accumulate blockchain. BVNs serve as their own roots of possible nodes, breaking up the job of validating transactions. BVN Sub-chains hold Merkle roots of chains collected and managed by a BVN. Effectively allows the sharding of BVN nodes, which in turn shard Accumulate.

### Directory Network (DN)

BVNs are tied together by a blockchain called the DN that builds directory blocks for Accumulate. The DN collects the summary hash for all the BVNs and puts them in a directory block for every block period. In this way, the DN acts as a directory service for Accumulate, and resolves questions about the state of Accumulate at every block. 

### Anchor Chain

A chain that aggregates anchors from other chain.
