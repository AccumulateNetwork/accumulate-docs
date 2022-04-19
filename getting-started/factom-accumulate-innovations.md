---
description: >-
  A quick summary of the innovations and advantages of Factom and Accumulate
  that greatly aid integrations of real world applications and use cases with
  the blockchain technology.
---

# Innovations

The Accumulate Protocol is being built by many of the core developers behind the [Factom Protocol](https://www.factomprotocol.org). Factom was one of the earliest blockchain protocols, being established back in 2014. Over the years there have been many advancements in the blockchain field. Accumulate is being developed to incorporate the early innovations of Factom while also learning from and applying lessons learned from these new advancements.

Here is a quick summary of the innovations and advantages of Factom and Accumulate that greatly aid integrations of real world applications and use cases with the blockchain technology.

* Factom's data based blockchain innovations:
  * User Chains -- Data organized in chains
  * Performance -- Scalable architecture
  * Two Token Architecture -- Separate, non-transferable credit tokens for fee payment
  * Anchoring -- Taps into cryptographic security of other blockchains
  * Cryptographic proofs of all blockchain contents against all anchors
* Accumulate's Identity based blockchain:
  * Key Management -- management of identities over time
  * Token issuance -- any identity can issue tokens
  * Token management -- tokens are held by identities, and sent to identities
  * Data management -- data chains are created and controlled by Identities
  * Scratch Space
    * Coordination -- multi-party transaction construction on the blockchain
    * Limited availability -- Not guaranteed after 20,000 blocks (about 2.3 weeks)
    * Segregated witness -- Bulky authorizations don’t bloat the blockchain
    * Blockchain rewriting -- Blends advantages of 10 second blocks with 10 minute blocks
  * Performance
    * Sharding -- Block Validator Networks (BVNs) and the Directory Block Network (DBN) run independently
    * Synthetic Transactions -- Transaction processing runs in parallel with blockchain syncronization
    * BVNs and DBN each run their own consensus (independently)
    * Tokens are tracked across accounts, one chain per account
    * All accounts can process transactions in parallel
    * All Identity validation can be processed in parallel
    * Tendermint Consensus will be run for each BVN and the DBN so that adding BVNs adds capacity very close to linearly
    * Tendermint capacity is about 1000 to 10,000 tps per BVN
    * State required to validate a chain is preserved on-chain; syncing with a chain for building or accessing the current state of the blockchain is nearly instant.
    * Maintaining the data and history of the blockchain is maintained on validator nodes separate from data nodes for accessing the past state of the blockchain
  * URLs
    * URL addressing of Accumulate identities, data, transactions, and state Traditional technology stacks easily integrate with URL addressable data and endpoints Much improved user experience Enables integration with browsers
    * Tokens can be sent to human readable URLs rather than odd collections of characters
