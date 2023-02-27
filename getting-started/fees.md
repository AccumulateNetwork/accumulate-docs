---
description: Learn about estimated fees for common actions on the Accumulate Protocol.
---

# Fees

Accumulates fees are fixed and stable. Business models, built on Accumulate, can rely on a predictable cost model to support their go-to-market strategies today and tomorrow.

Estimated fees below are converted to USD for actions like identity creation, token transactions, and token issuances.

| Type                      | Base Fee (credits) | Base Fee (USD, approx.) |
| ------------------------- | ------------------:| -----------------------:|
| Add Credits¹              |               0.00 |                 $0.0000 |
| Burn Credits¹             |               0.00 |                 $0.0000 |
| Transfer Credits          |               0.01 |                 $0.0001 |
| Send Tokens               |               3.00 |                 $0.0300 |
| Issue Tokens              |               3.00 |                 $0.0300 |
| Burn Tokens               |               0.10 |                 $0.0000 |
| Create Identity²          |             500.00 |                 $5.0000 |
| Create Token Account      |              25.00 |                 $0.2500 |
| Create ADI Data Account   |              25.00 |                 $0.2500 |
| Create Lite Data Account³ |               0.10 |                 $0.0010 |
| Create Token              |            5000.00 |                $50.0000 |
| Write Data³               |               0.10 |                 $0.0010 |
| Write Scratch Data³       |               0.01 |                 $0.0001 |
| Create Key Page           |             100.00 |                 $1.0000 |
| Create Key Book           |             100.00 |                 $1.0000 |
| Update Key Page           |               3.00 |                 $0.0300 |
| Sign Transaction          |               0.01 |                 $0.0001 |

¹Adding and burning credits have minimum amounts instead of a fee. Adding or burning less than 1 credit is prohibited.<br />
²For 8+ characters. See the [sliding fee schedule](#sliding-fee-schedule) for the cost of shorter ADIs.<br />
³Creating and writing to a Lite Data Account always costs 0.10 credits. Writing to an ADI Data Account normally costs 0.10 credits. Writing to an ADI Data Account costs 0.01 credits if the data is marked as scratch data. Lite Data Accounts do not support scratch data.<br />


#### Multi-Operation Transactions

* SendTokens, IssueTokens - charge 1.00 credit for each output after the first
  * One output costs 3, two costs 4, three costs 5, etc.
* UpdateKeyPage, UpdateAccountAuth - charge 1.00 credit for each operation after the first
  * One operation costs 3, two costs 4, three costs 5, etc.
* CreateKeyPage - charge 1.00 credit for each key after the first
  * One key costs 100, two costs 101, three costs 102, etc.
* Delegation - charge 0.01 credit for each layer of delegation
  * A basic (non-delegated) signature costs 0.01, a delegated signature costs 0.02, a double-delegated signature costs 0.03, etc.

#### Sliding fee schedule

Short ADIs cost more. The length of an ADI is calculated as the number of bytes of the UTF-8 encoded string minus the `.acme` suffix, _not the number of characters_. For example, `屋.acme` and `abc.acme` are both counted as 3 bytes long. The current schedule is:

| Length | Cost                     |
| ------ | ------------------------ |
| 1      | $48000 / 4800000 credits |
| 2      | $12000 / 1200000 credits |
| 3      | $3500 / 350000 credits   |
| 4      | $900 / 90000 credits     |
| 5      | $250 / 25000 credits     |
| 6      | $70 / 7000 credits       |
| 7      | $18 / 1800 credits       |
| 8+     | $5 / 500 credits         |

{% hint style="info" %}
All transactions incur a 0.1 credit fee per each 256 bytes over a base 256 bytes. The additional fee is 0.01 credits instead of 0.1 if it is a scratch transaction. Signatures incur a 0.01 credit fee for each 256 bytes over a base 256 bytes.
{% endhint %}

{% hint style="info" %}
Except for send tokens, failed transactions paying fees over 1 credit will be refunded less 1 credit. No refund is made for fees less than or equal to 1 credit.
{% endhint %}

{% hint style="info" %}
For send token transactions each failed output will refund 1 credit.&#x20;
{% endhint %}
