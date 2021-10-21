---
description: >-
  How to create an anonymous token address How to marshall the data for signing
  (i.e. how to generate your signature)
---

# Lite Accounts

**1.      Introduction**

Participation in the Accumulate network occurs through Accumulate Digital Identifiers (ADIs) and Lite Accounts, similar to how participation in other blockchains occurs through a wallet or address. ADIs, which were described previously in Use Cases and Technical Guides, give users access to the full range of features provided by the Accumulate network including smart contracts, offchain consensus building, and dynamic key management. Lite Accounts are a ‘lite’ version of ADIs that, despite their comparatively limited utility and flexibility, may appeal to users who simply want to send and receive tokens and maintain a record of their token accounts and transactions. Lite Accounts also fulfill several important roles, including ADI sponsorship, that will be discussed in the following sections. In this technical guide, we will expand on the utility of Lite Accounts and describe the process of their creation.

&#x20;

**2.      Differences Between ADIs and Lite Accounts**

**2.1    General Overview**

ADIs allow a user to manage data, tokens, and sub-identities over time using a set of prioritized keys. Depending on the level of security required, these keys may be owned by an individual or consortium and secured by a single signature or key set. High priority administrative keys can manage lower priority keys by changing security, reassigning ownership, and creating backups. For example, a business could update their existing keys to a new security protocol or revoke the key access of an employee after termination. Key hierarchies and subchains enable complex operations and make ADIs an attractive technology for individuals and enterprises alike who require flexibility in key management and the option to implement advanced security features.

A Lite Account may be considered a simplified version of an ADI that manages one type of token. Multiple accounts can be created by a single user to store multiple types of tokens, but the token type and security model of each account is permanently fixed. A lack of subchains and key hierarchies also means that Lite Accounts are independent, although two Lite Accounts can interact with each other through deposits and withdrawals just as users can interact through traditional blockchain addresses. While a user is directly involved in the creation of a Lite Account address through the naming of the ADI and its subchains, Lite Accounts are automatically created by the network once a transaction is sent from an external wallet. So long as the exchange can determine the public key hash, it can derive a Lite Accounts URL and send tokens to that account.

**2.2    Specific Features**

The URL for an ADI identifies the account name and the names of its associated subchains, which are all chosen and managed by the owner of the ADI. A Lite Account, in contrast, is identified solely by a token URL and public key hash, which is automatically derived from the Ed25519 public key. Thus its security is self-contained within the Lite Account and is not dependent on the key security provided by an ADI. In the future, the token issuance will determine what type of asymmetric key algorithm is used for Lite Accounts, but the security will remain fixed once the account is created. The security model of an ADI can be upgraded, downgraded, or even changed to a completely different algorithm.

Anyone can generate a Lite Account by arranging for tokens to be sent to a Lite Account address corresponding to a public key that they own. ADIs, in contrast, can only be created by a sponsor through the spending of non-transferable credits issued through the Accumulate protocol. A user without an ADI to use as a sponsor can buy ACME tokens on an exchange, create a Lite Account for ACME tokens, purchase credits on the network, and sponsor the creation of their own ADI. They can then use their ADI to sponsor the creation of additional ADIs for themselves or others.

** **

**3.      Building a Lite Account**

**3.1    General Mechanism**

A Lite Account consists of an identity and token URL. The Accumulate wallet automatically derives the identity by concatenating the SHA256 hash and checksum of a user’s public key. The token URL (e.g. bob/token) is specified by the user and appended to the identity. A Lite Account is created by the first transaction sent to its URL. This transaction may originate from an exchange or an external wallet (e.g. Metamask). When the Accumulate network receives the transaction, it will create a Lite Account if the Lite Account URL is valid and a Lite Account does not already exist for that URL.

To spend tokens in the Lite Account, a user will create a transaction, hash and sign it with their private key, attach their public key, and submit this to the Accumulate network. The network will hash the public key and compute a checksum, verify that hash and checksum is identical to the Lite Account provided by the user, then decrypt the signature with their public key and verify the withdrawal. The network trusts that the person that owns the private key that hashes to this string of characters is the one who signed this transaction.

**3.2     Architecture**

The URL format of a Lite Account is acc://\<keyHash>\<checkSum>/\<tokenUrl>. The \<keyHash> is the first 20 bytes of the SHA256 sum of the account’s public key, encoded as hexadecimal. The \<checkSum> is the last 4 bytes of the SHA256 sum of the lower case \<keyHash>, also encoded as hexadecimal. The following example illustrates the process of creating a Lite ACME token account from a public/private key pair:

_PrivKey: b270eaaa57e5d4d808a9766f64b340aa655481c298288238e5b1b3561fb80b27_

_PubKey: 023e6165e349c2822089ab042b3a885ca54a0907e237e8bfb5bd2aa96885966f3_

Compute the SHA256 hash of the public key:

_818D7C1F69E7BEBCE54FE087F44D86D14279100D2EEA690AC3847AE1B9A14237_

Trim hash to first 20 bytes (odds of random match is 1 in 10^48) and convert to lowercase

_818D7C1F69E7BEBCE54FE087F44D86D14279100D_

818d7c1f69e7bebce54fe087f44d86d14279100d

Compute checksum (last 4 bytes of SHA256 hash of trimmed hash) and convert to lowercase:

_904A336D_

_904a336d_

Concatenate (20 bytes of) the hash, the checksum, a slash, and the token URL:

_acc://_818d7c1f69e7bebce54fe087f44d86d14279100d904a336d_/acme_

The length of a Lite Account is fixed at 48 characters, where the hash of the public key occupies 40 characters and the appended checksum an additional 8 characters. Thus, the length of a Lite token account URL is also fixed, at 49 characters (1 for the slash) plus the length of the token URL. When submitting a transaction to a Lite Account, a user can choose whether to append the acc:// prefix. If a prefix is not added by the user, it will be automatically added by the network.

&#x20;

**4.      Security**

**4.1    Token Registries**

The names of ADIs and their subchains are chosen by the user. If a user creates an ADI based solely on the key hash from their Lite Account, this has the potential to confuse the user since some accounts will be Lite Accounts while others will be tied to ADIs. The creation of a token registry for all tokens associated with a public key hash will block its reuse and also provide a user with a record of their token accounts. While these accounts cannot be managed like ADIs, a registry will help a user keep track of their assets and minimize the chance that tokens in a particular account will be forgotten. A token registry creates a record of the public key hash in the Patricia Trie and a record of individual token accounts in the Merkle Tree that can be queried to provide a list of tokens held by an account at any point in time.

**4.2    Checksum**

Appending a checksum to the hash of the public key prevents the irreversible loss of tokens if public key hash is copied incorrectly or derived from another algorithm. When the server receives a transaction, it converts the Lite Account identity into bytes, takes the first 20 bytes that represents the key hash, and recalculates the checksum from the first 40 hexadecimal characters, and verifies if they match. If the checksum is incorrect, the transaction fails and tokens are returned to the sender. This process functions as a built-in verification mechanism, which is particularly important for Lite Accounts since they are not comprised of human readable text.
