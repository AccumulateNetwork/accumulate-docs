---
description: An overview of Accumulate's identity hierarchy
---

# Identity Hierarchies

**1. Introduction**

In the Technical Guide for Accumulate Digital Identifiers (ADIs), we differentiated ADIs from addresses typically encountered in other blockchains and introduced their nomenclature and architecture on the Accumulate network. In this guide, we’ll take a deeper look at how ADIs are constructed with a particular focus on the identity hierarchy.

ADIs are URL-based digital identities with hierarchical key sets that can manage data, tokens, and sub-identities. They can also be used for more complicated operations such as token issuance, off-chain consensus building, and multisignature transactions. While key hierarchies are useful for organizing priorities, identity hierarchies are useful for organizing objects. Objects might include different token types held by a user, different departments within an organization, or different data types collected by an array of IoT sensors. How a company organizes its departments, financial records, or data structures can be reproduced in the organization of objects on the Accumulate network.



**2. Accounts**

Data and token sub-chains are classified as accounts, while identity sub-chains are classified as sub-ADIs. Accounts have the general format \<prefix>://\<ADI>/\<designator>/\<account> where designators are an organizational tool that is used to specify a particular type of sub-chain. Several examples of data and token accounts are provided in the table below for the hypothetical ADI ‘bank’. Both cryptocurrencies and tokenized assets may be considered token sub-chains

| <p> </p><p><strong>Description</strong></p><p> </p> | <p> </p><p>Data</p><p> </p>                      | <p> </p><p>Tokens</p><p> </p>                  |
| --------------------------------------------------- | ------------------------------------------------ | ---------------------------------------------- |
| <p> </p><p><strong>Designator</strong></p><p> </p>  | <p> </p><p>d</p><p> </p>                         | <p> </p><p>t</p><p> </p>                       |
| <p> </p><p><strong>Sub-ADI-1</strong></p><p> </p>   | <p> </p><p>acc://bank/d/accounts</p><p> </p>     | <p> </p><p>acc://bank/t/loans</p><p> </p>      |
| <p> </p><p><strong>Sub-ADI-2</strong></p><p> </p>   | <p> </p><p>acc://bank/d/investments</p><p> </p>  | <p> </p><p>acc://bank/t/securities</p><p> </p> |
| <p> </p><p><strong>Sub-ADI-3</strong></p><p> </p>   | <p> </p><p>acc://bank/d/transactions</p><p> </p> | <p> </p><p>acc://bank/t/realestate</p><p> </p> |
| <p> </p><p><strong>Sub-ADI-N</strong></p><p> </p>   | <p> </p><p>acc://bank/d/data</p><p> </p>         | <p> </p><p>acc://bank/t/tokens</p><p> </p>     |

Accounts are terminal sub-chains, meaning that sub-accounts don’t exist. However, a user can choose a different designator to categorize objects so long as the object type is specified within their wallet. For example, an investment firm with ADI ‘firm’ may create data accounts with designators _r_ and _c_ residential and commercial properties, while a cryptocurrency trader and non-fungible token (NFT) art collector may create token accounts with designators _n_ and _s_ to denote NFTs and stablecoins.

| <p> </p><p><strong>Description</strong></p><p> </p> | <p> </p><p>Data</p><p> </p>                    | <p> </p><p>Data</p><p> </p>             |
| --------------------------------------------------- | ---------------------------------------------- | --------------------------------------- |
| <p> </p><p><strong>Designator</strong></p><p> </p>  | <p> </p><p>Variable</p><p> </p>                | <p> </p><p>Variable</p><p> </p>         |
| <p> </p><p><strong>Sub-ADI-1</strong></p><p> </p>   | <p> </p><p>acc://firm/r/properties</p><p> </p> | <p> </p><p>acc://user/n/art</p><p> </p> |
| <p> </p><p><strong>Sub-ADI-2</strong></p><p> </p>   | <p> </p><p>acc://firm/c/sales</p><p> </p>      | acc://user/s/USDT                       |

****

**3. Sub-ADIs**

The structure of identity subchains for sub-ADIs is similar to those of an account, where any number of sub-ADIs can be nested under a designator that a user defines in their wallet as an identity. However, sub-ADIs can also be nested under other sub-ADIs. The format of an identity chain with multiple sub-ADIs is \<prefix>://\<ADI>/{\<designator>/< subN-ADI>}N where N refers to an arbitrary number of sub-ADIs each with the same identity designator. In the example below, different departments within a bank are represented by different Sub-ADIs.

| <p> </p><p><strong>Description</strong></p><p> </p> | <p> </p><p>Identity</p><p> </p>           |
| --------------------------------------------------- | ----------------------------------------- |
| <p> </p><p><strong>Designator</strong></p><p> </p>  | <p> </p><p>i</p><p> </p>                  |
| <p> </p><p><strong>Sub-ADI-1</strong></p><p> </p>   | <p> </p><p>acc://bank/i/hr</p><p> </p>    |
| <p> </p><p><strong>Sub-ADI-2</strong></p><p> </p>   | <p> </p><p>acc://bank/i/legal</p><p> </p> |
| <p> </p><p><strong>Sub-ADI-3</strong></p><p> </p>   | <p> </p><p>acc://bank/i/sales</p><p> </p> |
| <p> </p><p><strong>Sub-ADI-N</strong></p><p> </p>   | <p> </p><p>acc://bank/i/tbd</p><p> </p>   |

The human resources department can be** **further subdivided into sub-ADIs that specify different roles within the department.

| <p> </p><p><strong>Description</strong></p><p> </p> | <p> </p><p>Identity</p><p> </p>                             |
| --------------------------------------------------- | ----------------------------------------------------------- |
| <p> </p><p><strong>Designator</strong></p><p> </p>  | <p> </p><p>i</p><p> </p>                                    |
| <p> </p><p><strong>Sub1-ADI-1</strong></p><p> </p>  | <p> </p><p>acc://bank/i/hr</p><p> </p>                      |
| <p> </p><p><strong>Sub2-ADI-1</strong></p><p> </p>  | <p> </p><p>acc://bank/i/hr/i/cpo</p><p> </p>                |
| <p> </p><p><strong>Sub3-ADI-1</strong></p><p> </p>  | <p> </p><p>acc://bank/i/hr/i/cpo/i/director</p><p> </p>     |
| <p> </p><p><strong>SubN-ADI-1</strong></p><p> </p>  | <p> </p><p>acc://bank/i/hr/i/cpo/i/director/tbd</p><p> </p> |

****

**4. Combining Accounts and Sub-ADIs**

Data and token accounts may also be nested within sub-ADIs. This offers an alternative strategy for organizing large numbers of data and token accounts without needing to change the designator. Using the example of an investment firm that manages different types of properties, we can imagine that a team specializing in residential homes may be given a different sub-ADI than a team specializing in commercial real-estate. For simplicity, we refer to these combined addresses simply as URLs below.

| <p> </p><p><strong>Description</strong></p><p> </p> | <p> </p><p>Variable</p><p> </p>                                      |
| --------------------------------------------------- | -------------------------------------------------------------------- |
| <p> </p><p><strong>Designator</strong></p><p> </p>  | <p> </p><p>Variable</p><p> </p>                                      |
| <p> </p><p><strong>URL-1</strong></p><p> </p>       | <p> </p><p>acc://firm/i/residential/d/properties</p><p> </p>         |
| <p> </p><p><strong>URL-2</strong></p><p> </p>       | <p> </p><p>acc://firm/i/commercial/i/office/d/properties</p><p> </p> |
| <p> </p><p><strong>URL-3</strong></p><p> </p>       | <p> </p><p>acc://firm/i/commercial/t/securities</p><p> </p>          |

Since accounts are terminal sub-chains, it is not possible to nest sub-ADIs within accounts. While acc://firm/i/residential/d/properties is permitted, acc://firm/d/properties/i/residential is not.

&#x20;

**5. Development Timeline**

For Testnet 1.0, users will only be able to create top-level ADIs and ADI token accounts. However, designators and sub-ADIs will be introduced in later versions of the Testnet to allow an organization to create identity hierarchies and manage keys held by sub-ADIs. Multiple accounts can be managed by a single ADI in Testnet 1.0, and multiple ADIs will be able to manage a single data or token account in Testnet 2.0. For example, a consortium of banks with different ADIs will be able to manage a tokenized asset like a bundle of real-estate.
