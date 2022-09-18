# Glossary

### A

#### Accumulate

The Accumulate network is a collection of independent chains. Each chain is managed by a hierarchy of identities known as Accumulate Digital Identifiers (ADIs), and each identity possesses a hierarchy of keys, which allows it to participate in the execution of transactions.

#### ACME

“ACME” is the symbol of a cryptographic token used in the Accumulate protocol. The ACME token, which is a traditional spendable token, like ETH and BTC and it is issued by the protocol to reward those providing services to the protocol. For example, Validators will be awarded staking fees in ACME.

#### Accumulate Blocks

The Accumulate protocol defines minor blocks and major blocks. Minor blocks are once per second synchronization points of the Merkle trees. Major blocks are twice per day.

#### Accumulate Digital Identifier (ADI)

ADIs allow smart contracts, consensus building, validator networks, and enterprise-level management of digital assets that go beyond the simple and constrained smart contract-based frameworks of other blockchains. Also, an Identity or Accumulate Digital Identifier is a human readable URL that can represent users, institutions, devices and Identity has accounts which holds its assets, whether that is tokens, data, or keys.

#### ADI Data Account

An ADI Data Account is one of the types of accounts an ADI can control. An ADI data account holds data. An ADI data account can be represented as so:

acc://Bob/Data

To write Data you would specify this URL.

#### ADI Token Account

An ADI Token Account is one of the types of accounts an ADI can control. An ADI token account holds tokens. An ADI token account can be represented as so:

acc://Bob/Tokens/ACME

When you are sending or receiving tokens you would specify this URL.

#### ADI Scratch Data Accounts (Scratch Chains)

Scratch chains are identical to data chains, however, after 2-3 weeks the chain is compressed, and proof of the transactions is created. A proof is a logical argument used to show the truth of the operations made on the chain. This argument or proof contains less data than the scratch chain it is representing. This allows the blockchain to not be burdened with moving substantial amounts of data over the network.

### B

#### Block Validator Network (BVN)&#x20;

A BVN executes transactions against records. At the end of each block, the BVN collects Merkle DAG roots (anchors) from the transaction chain of records modified by one or more transactions in the block, appending them to the BVN’s root chain. The anchor from the root chain is sent to the DN.&#x20;

#### Block Validator Network Node (BVNN)&#x20;

A BVNN is a node with a BVN.

### C

#### Chain Validators/Executors

Chain validators can be thought of as transaction executors. The actual code for executors is per-transaction (type), not per-chain. As an example, the creation of an identity would have a specified executor. The validation of the signature for instance is handled by the overall validator/executor.

#### Credits

Credits are a non-transferable form of payment on the Accumulate Network. Credits are created by converting ACME tokens into credits. Once the user converts ACME tokens to purchase credits, credits are used for actions on the network, such as creating an ADI, ADI Token Account, or Updating Keys in a Key Page.

### D

#### Directory Network (DN)

The DN executes transactions against certain system records, such as the ACME token issuer. The DN also receives root chain anchors from BVNs, appending them to the DN’s BVN anchor chain. At the end of each block, the DN collects Merkle DAG roots (anchors) from the transaction chain of records modified by one or more transactions in the block (including the DN’s BVN anchor chain), appending them to the DN’s root chain. The anchor from the root chain is sent to all of the BVNs.&#x20;

#### &#x20;Directory Network Node (DNN)

A DNN is a node within a DN.

### K

#### Keys

Keys are defined as the hash of the public key for a signature.

#### Key Book

Key Books store an ADI's Hierarchical Key Management Structure using Key Pages and Keys within those pages. A Key Book is an ordered set of Key Pages by priority where any Key Page can modify itself or a Page of lower priority. Modifications include adding, updating, or removing keys. An account specifies what Key Book applies to any transaction within that account.

A Key Book can be represented as so:\
\
acc://Bob/KeyBook

#### Key Page

A Key Page defines the set of Keys required to validate a transaction. A Key Page specifies one or more Keys possible and how many such Keys are required to validate a transaction. For example, a Key Page with an m of n of 3 of 4 means that the page contains 4 keys, and 3 of those 4 keys are required to sign transactions. This transaction would be considered multi-sig, whereas an m of n of 1 of 1 would be single-sig. Key Pages store credits.

### L

#### Layer-1 Anchoring

An anchor is created from the latest Directory Network major block, which is then anchored into a Layer 1 Blockchain such as Bitcoin.

#### Lite Data Chain

A lite data chain is a chain that anyone can write data to, as opposed to ADI Data Accounts which requires specified keys.

#### Lite Token Account

A lite token account is an unstructured account similar to an address such as Bitcoin, a string of non-human readable characters. Lite Token Accounts are free to create. Accumulate represents these accounts as so:

acc://bf3c639bbce4f523897050de8df9f34f49d8be7d9eb8fa11/ACME

Lite Token Accounts are not associated with an identity and are not acknowledged by the Accumulate network until they have ACME tokens.

### M

#### Major Blocks

Every 12 hours, the transactions executed in the last 12 hours (since the prior major block) are collected into a new major block. For each record modified by a transaction in the block, a Merkle DAG root (anchor) is taken from the main transaction chain of the record and appended to the DN or BVN’s major root chain.

#### Managed Chain (Authorities)

When creating an ADI account, you can specify an additional Key Book within the same ADI that manages a Key Book. As an example, a transaction submitted using Key1 from acc:/Bob/KeyPage1 within acc://Bob/ KeyBook1 would be routed to acc:/Bob/KeyBook2 which is manager for that account. The manager would then need to sign a transaction approving the transactions specified by the Key Page and m of n required. In the future a Key Book of one ADI will be able to manage a Key Book of another ADI.

#### Minor Blocks

Tendermint collects incoming transactions and presents them to the application in blocks, generally once per second. These are minor blocks. At the end of each minor block, for each record that was modified by a transaction within the block, a Merkle DAG root (anchor) is taken from the main transaction chain of the record and appended to the DN or BVN’s minor root chain.

### P

#### Pending Chains

A pending chain tracks transactions that haven’t been promoted to the main chain. For example, a multi-signature with an `m` of `n` and 3 of 4, with only two signatures, would sit in the pending chain until 3 of 4 were signed. In addition, if a manager hasn’t signed a transaction, the transactions would sit in the pending chain until the specified m of n was satisfied. Finally, the data produced in the pending chain is trimmed every 2.3 weeks.

### S

#### Scratch Space

Accumulate provides scratch space on the blockchain that can be used by parties to come to consensus, but whose data availability is not retained by Accumulate forever. Scratch space allows processes to provide cryptographic proof of validation and process transactions without overburdening the blockchain.

#### Sub-ADI

An ADI can contain another ADI. We call this a sub-ADI. While an ADI contains accounts, a sub-ADI contains sub-accounts.

#### Synthetic Transactions

Synthetic transactions are any transactions that are generated by the protocol. These include transactions that deposit tokens into other token accounts and refund amounts for failed transactions.

### T

#### Token Issuance

In Accumulate, users will be able to create custom tokens that can be used within the Accumulate protocol.
