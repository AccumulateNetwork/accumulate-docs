# Protocol Overview

### Abstract

Accumulate is a highly unique blockchain network built to address the biggest fundamental issues with blockchain technology: security, validation, scaling, pruning, and integration. Accumulate is the first blockchain to be completely organized around Decentralized Digital Identity and Identifiers \(DDIIs\). Accumulate Digital Identifiers \(ADIs\) have powerful and novel uses within Accumulate to allow the blockchain network to be applied to a huge set of use cases. ADIs allow smart contracts, consensus building, validator networks, and enterprise level management of digital assets that goes beyond the simple and constrained smart contract based frameworks of other blockchains. 

Accumulate anticipates a world where the blockchain is a network of blockchain services, data, and endpoints for processes supporting payments, business, education, regulation, entertainment, social networks and more. To this end, Accumulate will be the first indexable blockchain using URLs to index anything within Accumulate.

### Introduction

A typical blockchain is organized around addresses, as pioneered by Bitcoin, the first blockchain. Addresses are usually controlled by a public/private key pair. In this case, addresses \(or accounts\) are a hash or partial hash of the public key. This hides the public key until some spend occurs, identifying the address as based on a particular public/private key pair. Other options exist, such as smart contracts with Ethereum. In this case the account is the basis for calling functions against the smart contract and potentially updating its state.

Blockchains use smart contracts to expand blockchains beyond simple exchanges of tokens, making the exchange of tokens dependent on more complex calculations using data and inputs from multiple users. Naturally, the data on the blockchain is pretty limited when it comes to interacting with the real world, creating a need for trusted oracles to provide real world data to the blockchain.

Many blockchains seek to scale transactions and smart contracts through various approaches to sharding and parallel processing. Networks of independent blockchains can do so, since independent chains don’t interact at the verification layer. Dependencies in processes important to users are handled by external mechanisms. The risks of trusting such external mechanisms is restricted to those blockchain users that choose to depend on externalities.

In the case of tokens of one blockchain being traded on another chain or side-chain, the security of using tokens with characteristics defined off chain depends on the processes used to communicate between chains. Smart contracts can embed some of these processes on chain, but cannot fully secure the communication between independent chains, since validation of what happens on one chain cannot serve as inputs for a smart contract on another chain.

One mechanism used by many smart contract based protocols is to define bonds to penalize malfeasance in the communication between independent chains. Bonds are being used today for validators. Still, creating cryptographic proofs of malfeasance to apply penalties is challenging. The parties that validate information across the chains can be viewed as validators. Parties that validate their performance can be viewed as auditors.

Accumulate takes a pragmatic approach to defining the risk and independence of transactions across the protocol by using short block sizes and adding latency between the validation and recording of transactions, and the application of the outcome of a transaction to the state of the blockchain.

Accumulate processes transactions as submitted by users of the protocol directly, but rather than these changing the state of the blockchain, user transactions create synthetic transactions that are then processed by the protocol. Because user transactions are limited to changing only one part of the protocol, they can almost always be processed in parallel. Since synthetic transactions are limited to changing only one part of the protocol, they too can be processed in parallel in following blocks.

Accumulate is built around Accumulate Digital Identities \(ADIs\). ADIs are identifiers specified by the users and applications that build them. The keys that manage ADIs are separate, and can be managed over time. The keys to an ADI can be managed \(like signers on an account\) so that new ADIs don’t have to be issued just because a company must shift responsibilities over time. The departure of an employee should not require new ADIs, just new security.

Even the technology of keys and signing should allow upgrades in Accumulate without major upending of the actual ADIs.

Accumulate also anticipates the need for ADIs to manage identities, processes, tokens, and data. Everything in Accumulate can be addressed through UDIs. Applying Internet standards for addressing and routing to the blockchain allows blockchains to scale just as the Internet has proven to be able to scale.

One of the issues with much security in blockchains is the off blockchain processes that are needed to arrive at an entry on the blockchain. Developers are faced with a trade off between the expense and difficulty of showing their work on the blockchain, and the lack of accountability when the work of coming to consensus is done off blockchain.

Accumulate provides scratch space on the blockchain that can be used by parties to come to consensus, but whose data availability is not enforced by Accumulate forever. Scratch space allows processes to provide cryptographic proof of validation and process without over burdening the blockchain.



## 



