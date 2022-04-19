---
description: An overview of Accumulate's identity hierarchy
---

# Identity Hierarchies

This guide will take a deeper look at how the construction of ADIs with a focus on the identity hierarchy.

ADIs are URL-based digital identities with hierarchical key sets that can manage data, tokens, and sub-identities. They can also be used for more complicated operations such as token issuance, off-chain consensus building, and multi-signature transactions. While key hierarchies help organize priorities, identity hierarchies help organize objects.&#x20;

Objects might include:

* Different token types held by a user,
* Different departments within an organization,&#x20;
* Different data types collected by an array of IoT sensors.&#x20;

How a company organizes its departments, financial records, or data structures can be reproduced in the organization of objects on the Accumulate network.

**Accounts**

Data and token sub-chains are classified as accounts, while identity sub-chains are classified as sub-ADIs. Accounts have the general format \<prefix>://\<ADI>/\<designator>/\<account> where designators are an organizational tool used to specify a particular type of sub-chain. Several examples of data and token accounts are provided in the table below for the hypothetical ADI ‘bank’. Both cryptocurrencies and tokenized assets may be considered token sub-chains

| **Description** | Data                      | Tokens                  |
| --------------- | ------------------------- | ----------------------- |
| **Designator**  | d                         | t                       |
| **Account-1**   | acc://bank/d/accounts     | acc://bank/t/loans      |
| **Account-2**   | acc://bank/d/investments  | acc://bank/t/securities |
| **Account-3**   | acc://bank/d/transactions | acc://bank/t/realestate |
| **Account-N**   | acc://bank/d/data         | acc://bank/t/tokens     |

Accounts are terminal sub-chains, meaning that sub-accounts don’t exist. However, users can choose a different designator to categorize objects so long as the object type is specified within their wallet. For example, an investment firm with ADI ‘firm’ may create data accounts with designators _r_ and _c_ residential and commercial properties. In contrast, a cryptocurrency trader and non-fungible token (NFT) art collector may create token accounts with designators _n_ and _s_ to denote NFTs and stable coins.

| **Description** | Data                    | Data              |
| --------------- | ----------------------- | ----------------- |
| **Designator**  | Variable                | Variable          |
| **Account-1**   | acc://firm/r/properties | acc://user/n/art  |
| **Account-2**   | acc://firm/c/sales      | acc://user/s/USDT |

***

**Sub-ADIs**

The structure of identity subchains for sub-ADIs is similar to an account. sub-ADIs can be nested under a designator that users define in their wallet as an identity. However, sub-ADIs can also be nested under other sub-ADIs. The format of an identity chain with multiple sub-ADIs is:///{/< subN-ADI>}N, where N refers to an arbitrary number of sub-ADIs each with the same identity designator. In the example below, different departments within a bank are represented by different Sub-ADIs.

| **Description** | Identity           |
| --------------- | ------------------ |
| **Designator**  | i                  |
| **Sub-ADI-1**   | acc://bank/i/hr    |
| **Sub-ADI-2**   | acc://bank/i/legal |
| **Sub-ADI-3**   | acc://bank/i/sales |
| **Sub-ADI-N**   | acc://bank/i/tbd   |

The human resources department can be\*\* \*\*further subdivided into sub-ADIs that specify different roles within the department.

| **Description** | Identity                             |
| --------------- | ------------------------------------ |
| **Designator**  | i                                    |
| **Sub1-ADI-1**  | acc://bank/i/hr                      |
| **Sub2-ADI-1**  | acc://bank/i/hr/i/cpo                |
| **Sub3-ADI-1**  | acc://bank/i/hr/i/cpo/i/director     |
| **SubN-ADI-1**  | acc://bank/i/hr/i/cpo/i/director/tbd |

***

**Combining Accounts and Sub-ADIs**

Data and token accounts may also be nested within sub-ADIs. This offers an alternative strategy for organizing large numbers of data and token accounts without needing to change the designator. Using the example of an investment firm that manages different types of properties, we can imagine that a team specializing in residential homes may be given a different sub-ADI than a team specializing in commercial real estate. For simplicity, we refer to these combined addresses simply as URLs below.

| **Description** | Variable                                      |
| --------------- | --------------------------------------------- |
| **Designator**  | Variable                                      |
| **URL-1**       | acc://firm/i/residential/d/properties         |
| **URL-2**       | acc://firm/i/commercial/i/office/d/properties |
| **URL-3**       | acc://firm/i/commercial/t/securities          |

Since accounts are terminal sub-chains, it is not possible to nest sub-ADIs within accounts. While acc://firm/i/residential/d/properties is permitted, acc://firm/d/properties/i/residential is not.

**Development Timeline**

For Testnet 1.0, users will only be able to create top-level ADIs and ADI token accounts. However, designators and sub-ADIs will be introduced in later versions of the Testnet to allow an organization to create identity hierarchies and manage keys held by sub-ADIs. In addition, multiple accounts can be managed by a single ADI in Testnet 1.0, and multiple ADIs will be able to manage a single data or token account in Testnet 2.0. For example, a consortium of banks with different ADIs will be able to manage a tokenized asset like a bundle of real estate.
