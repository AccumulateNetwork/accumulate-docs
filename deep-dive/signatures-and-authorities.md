# Signatures and authorities

{% hint style="info" %}
This document does not discuss types of votes and thresholds other than acceptance votes and acceptance thresholds. Other types of votes and thresholds are planned but not implemented. This document assumes all authorities are enabled and does not discuss disabled authorities.
{% endhint %}

## Definitions

#### Authority

Every account is governed by one or more authorities. An account's authorities decide whether transactions will be executed against that account.

In the subjective sense, 'an authority' refers to the authorities of some account. In the objective sense, 'an authority' refers to an account that can be the authority of other accounts.

#### Signer

A signer belongs to some authority and signs transactions on behalf of that authority. A signer specifies a set of signing keys. A signer may delegate to another authority.

#### Local vs Remote

Two accounts are local to each other if they belong to the same root identity (usually an ADI). Two accounts are remote to each other if they belong to different root identities. An authority may be local or remote to accounts it governs.

#### Direct vs Delegated

If an authority is listed in the authority set of an account, that authority is a _direct authority_ of the account. If an authority is a delegate of an account's authority, the former is a _delegated authority_ of the account.

Direct vs delegated is orthogonal to local vs remote, meaning you can have a local direct authority, a remote direct authority, a local delegated authority, or a remote delegated authority.

#### Key books and pages

A key book is a type of authority (in the objective sense). A key page is a type of signer. A key book contains one or more key pages. A key page contains one or more entries. Each entry specifies a public key hash and/or the URL of a delegate.

By default, a key book is governed by itself. However this can be changed, at time of creation or after.

A key page is always a direct child of the key book it belongs to, therefore a key page cannot be remote to its book.

#### Lite identities

A lite identity is both an authority and a signer (belonging to itself). A lite identity's URL is derived from a public key hash. No other keys can be used with a lite identity.

A lite identity is implicitly its own authority and the authority of any lite token accounts under it. The authority set of lite identities and lite token accounts is immutable.

A lite identity cannot delegate its authority nor can it be a delegate of another authority. A lite identity cannot be the authority of an ADI account. Since are no other types of authorities or signers, ADI accounts may only be governed by key books, key books may only govern ADI accounts, and delegates must be key books.

## Signature processing

A transaction is accepted once _all_ of the principal's authorities accept the transaction. An authority accepts the transaction once _any_ of its signers accept the transaction. A signer accepts the transaction once its conditions are met. A lite identity has no conditions and accepts the transaction as soon as a valid signature is received. A key page accepts the transaction when it has received a sufficient number of signatures to reach it's acceptance threshold.

Each entry of a key page may only sign a transaction once. If additional signatures are received, they are ignored. If an entry has both a public key hash and a delegate, either the key or the delegate may sign, but any subsequent signature via the other path is ignored. If a key page is updated (if its version increments) before it has accepted a transaction, all existing signatures are discarded and the transaction must be re-signed.

An authority effectively votes as a bloc. If a signer delegates to a multisig authority (e.g. a key book with a single page with M>1), the delegate does not submit its vote to the signer until the delegate's acceptance threshold is met.

Once an authority is satisfied, it submits its vote as a signature set to the principal (if it is a direct authority) or to the delegator (if it is a direct authority). If the authority and principal/delegator are remote to each other, the signature set must be forwarded to the principal/delegator via a SyntheticForwardTransaction.
