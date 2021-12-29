# Synthetic Transactions

**1. Introduction to Database Scaling**

How a business chooses to store and process its customer data largely depends on the size of the database, its read/write volume, and the availability requirements of its data. A small business may find it more convenient and economical to store its data in a database handled by a single server and vertically scale its hardware by upgrading its RAM, CPU, and storage capacity. It may also choose to replicate its database across multiple servers to make its data available even if some hardware fails or a server crashes. However, vertical scaling is not a viable option for a larger organization like Facebook, which generates upwards of 4 petabytes of data per day.

Instead, large and data-centric corporations often use a horizontal scaling strategy called sharding that distributes a single dataset across multiple databases and stores these databases on multiple servers or nodes. With this architecture, scalability and throughput are no longer limited by hardware but by capacity. Adding capacity by installing additional servers allows a database to scale, while distributing the data across different shards increases throughput by allowing parallel read/write operations.

**2. Scaling Solutions in Blockchain**

Blockchain also utilizes a form of horizontal scaling and that relies on a system of rewards for those who do the work of validating transactions and securing the network. Stakers in Proof of Stake (PoS) blockchains and miners in Proof of Work (PoW) blockchains lend their tokens or computational power to confirm transactions. Full node operators for PoS blockchains store copies of the entire blockchain and secure the network, receiving rewards at the risk of losing their stake if they engage in bad behavior.

A major difference in database management between traditional enterprises and blockchain protocols is decentralization of the latter. Unfortunately, this also introduces the Scalability Trilemma, which can be defined as a trade-off between decentralization, security, and scalability. Bitcoin, for example, chose security over scalability when it introduced a delay in the form of blocks. EOS, meanwhile, chose scalability at the cost of decentralization.

**3. Scaling Solutions in Accumulate**

Accumulate bypasses the trilemma by organizing itself around digital identities (e.g. ADIs, Lite Accounts) and treating each identity as an independent blockchain. All identities and the data contained within can be operated upon independently by design through the use of transaction flows and a series of networks operating in parallel, called the Block Validator Networks (BVNs).

Each BVN is a network of Tendermint nodes responsible for validating transactions on an identity chain. Each identity chain is assigned to a particular BVN, and as more identities are created, more BVNs can be added to scale the network and maintain high throughput. The summary hashes of an identity chain’s current state are anchored to the BVN. Meanwhile, each BVN is anchored to an Accumulate Directory Network (DN), which is responsible for coordinating the BVNs and guaranteeing security for the network. Security is further enhanced by anchoring the DN to a secondary blockchain such as Ethereum or Bitcoin to gain the added security provided by those networks.

While each identity acts as its own independent blockchain, transactions between the BVNs that host these identities necessitate a query of the sender’s transaction history to determine if they actually possess the assets they wish to send. Since no BVN contains the entire state of the Accumulate network, each BVN must be independently queried. As more BVNs are added to scale the network, the majority of queries will involve BVNs that have no transaction history with the sender. This puts unnecessary load on each BVN, which increases transaction cost and decreases transaction throughput.

To solve this problem, a third type of node network is introduced, called the Data Server Network (DSN). The DSN, does not have the requirement of high validation throughput. It will move the transaction data from the BVN’s and organize the transaction history into organized identity chains. Thus, this reduces the resource load on the BVN nodes, enabling the BVN’s to focus on managing the identity states, while allowing the DSN to maintain the transaction history for those states.

**4. Introduction to Synthetic Transactions**

To optimize transaction throughput, Accumulate uses synthetic transactions, which can be broadly defined as any transaction that is submitted by the protocol rather than by the user. To understand how synthetic transactions work, consider the classic example of Alice, Bob, and Charlie who will be treated as separate ADIs on the Accumulate network.

Alice’s transactions are handled by BVN-1, Bob’s by BVN-2, and Charlie’s by BVN-3. Bob needs to pay Charlie, but he can only do so once Alice pays him back. Alice sends a transaction to Bob after BVN-1 verifies that Alice has sufficient funds. Bob receives the tokens and sends a transaction to Charlie through BVN-2. However, BVN-2 doesn’t know about the transaction or from which BVN it came since Alice sent her transaction through BVN-1. Therefore, BVN-2 will have to query all other BVNs to verify that Bob has enough money to pay Charlie. This problem can be resolved by creating transaction flows with synthetic transactions.

After BVN-1 has validated Alice’s transaction, it sends a second transaction to BVN-2 that says, “Deposit X tokens into Bob’s account”. The transaction that BVN-1 sends to BVN-2 is called a synthetic transaction. Now both BVNs have a complete record of everything that has happened to their respective chains, and future transactions involving these chains will not require either BVN to query others in the Accumulate network. To ensure that no fake synthetic transactions can be injected into the system by an external player, the DN is used to produce cryptographic receipts for validating synthetic transactions. Thus, only valid synthetic transactions produced by the validators on a BVN can be processed and validated.

**5. Processing Synthetic Transactions**

The illustration below shows individual synthetic transactions between identities A-F that are being collected and sent as a bulk synthetic transaction from BVN-0 to BVN-1, BVN-2, and the Directory Network (DN). The yellow circles in rows A-F represent transactions, while those in the “Synthetic TX” row represent sets of transactions between identities A-F. The quadrangle that connects ADIs A-F, BVN-1, BVN-2, and the DN represents communication between all ADIs hosted on BVN-0 and all identities hosted on other BVNs or the DN. If the box representing BVN-1 were opened, for example, you might find identities G-J.

![](<../.gitbook/assets/Synthetic-Transactions-Figure3 (1) (1).svg>)

When a transaction or set of transactions validates on the Accumulate network, those transaction are duplicated as synthetic transactions that essentially export updates to other BVNs. Those updates do not require state in BVN-0 to validate what they should do in BVN-1, BVN-2, or the DN. If BVN-0 is sending a transaction to BVN-1, and later on to BVN-2, BVN-0 can operate at full speed and interact with BVN-2 without having to wait on BVN-1 to accept the deposit.

A real-world analogy would be the process of settling a credit card transaction. When a customer makes a purchase with their credit card, the credit card validates the transaction at the point of sale and the goods are released by the merchant. However, the merchant doesn’t have access to the customer’s money until the transaction settles. We’ll imagine that the credit card platform is hosted on BVN-0, and the merchant’s bank account is hosted on BVN-1. The customer can use their credit card for other purchases before the merchant’s bank accepts their payment because the customer’s credit card platform has sent a synthetic transaction to the bank broadcasting a summary of its transactions that we refer to an account balance.

**6. Conclusion**

For most blockchains, the transaction is the settlement. This is possible because most blockchains store the entire state of their network on full nodes. While this simplifies the process of validation, it also limits scalability. Accumulate is sharded by design, with each identity acting as an independent blockchain and every transaction on its chain being handled by a particular BVN. This revolutionary architecture allows the network to scale indefinitely through the addition of BVNs, but scalability is limited by increasingly inefficient communication as the network grows. Synthetic transactions provide a means of efficient communication between BVNs and add settlement to the blockchain.
