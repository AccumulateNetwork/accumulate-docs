---
description: Learn about estimated fees for common actions on the Accumulate Protocol.
---

# Fees

Accumulates fees are fixed and stable. Business models, built on Accumulate, can rely on a predictable cost model to support their go-to-market strategies today and tomorrow.

Estimated fees below are converted to USD for actions like identity creation, token transactions, and token issuances.

<table><thead><tr><th>Type</th><th data-type="number">Base Fee in Credits (approx.)</th><th>Fee in USD</th></tr></thead><tbody><tr><td>Create Identity</td><td>500</td><td>$5.00</td></tr><tr><td>Create Token Account</td><td>25</td><td>$0.25</td></tr><tr><td>Send Tokens</td><td>3</td><td>$0.03</td></tr><tr><td>Create ADI Data Account</td><td>25</td><td>$0.25</td></tr><tr><td>Write Data (ADI Data Account)</td><td>0.1</td><td>$0.001</td></tr><tr><td>Write Data (Scratch Chain)</td><td>0.01</td><td>$0.0001</td></tr><tr><td>Create/Write Data to (Lite Data Account</td><td>0.1</td><td>$0.001</td></tr><tr><td>Acme Faucet</td><td>0</td><td>$0.00</td></tr><tr><td>Create Token</td><td>5000</td><td>$50.00</td></tr><tr><td>Issue Tokens</td><td>3</td><td>$0.03</td></tr><tr><td>Burn Tokens</td><td>0</td><td>$0.00</td></tr><tr><td>Create Key Page</td><td>100</td><td>$1.00</td></tr><tr><td>Create Key Book</td><td>100</td><td>$1.00</td></tr><tr><td>Add Credits</td><td>0</td><td>$0.00</td></tr><tr><td>Update Key Page</td><td>3</td><td>$0.03</td></tr><tr><td>Sign Transaction</td><td>0.1</td><td>$0.001</td></tr></tbody></table>



* SendTokens, IssueTokens - charge 1.00 credit for each output after the first
  * One output costs 3, two costs 4, three costs 5, etc
* UpdateKeyPage, UpdateAccountAuth - charge 1.00 credit for each operation after the first
  * One operation costs 3, two costs 4, three costs 5, etc
* CreateKeyPage - charge 1.00 credit for each key after the first
  * One key costs 100, two costs 101, three costs 102, etc
* Delegation - charge 0.01 credit for each layer of delegation
  * A basic (non-delegated) signature costs 0.01, a delegated signature costs 0.02, a double-delegated signature costs 0.03, etc

{% hint style="info" %}
All transactions incur a 0.1 credit fee per for each 256 bytes over a base 256 bytes.
{% endhint %}

{% hint style="info" %}
Failed transactions paying fees over 1 credit will be refunded less 1 credit. No refund is made for fees less than or equal to 1 credit.
{% endhint %}
