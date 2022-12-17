---
description: This article will show you how to stake your ACME tokens.
---

# How to Stake your Tokens

{% hint style="info" %}
**Staking tokens gives custody of those tokens over to the staking system** unless and until they are unstaked.
{% endhint %}

The following steps will walk you through you how to set up your staking account for **delegated staking**.&#x20;

### Step 1: Install the CLI Wallet

#### There are two methods for setting up the CLI Wallet.&#x20;

1. _Installing from the source_ – requires a command line interface (e.g., Terminal or PowerShell), git and go.&#x20;
2. _Installing from binary-only_ requires a command line interface (e.g., Terminal or PowerShell))&#x20;

For instructions on setup using either method, go to the [CLI Setup Guide](../cli/cli-setup.md):

{% hint style="info" %}
If you use the binary method to set up your CLI, replace the word accumulate with whatever name appears after you drag-and-drop the binary onto your command line for the below commands. &#x20;
{% endhint %}

### Step 2: Make sure your accounts are set up

Before you can stake your ACME tokens, you must have the following setup:

* An ADI Token account for staking
* An ADI Token account for rewards (if you'd like to keep them in a separate account)

If you have not yet created your ADI, follow the instructions [here.](../tutorials/create-an-adi-via-cli.md)&#x20;

#### If you have not yet created the token accounts, run the following command to do so:

```
accumulate account create token <yourAdi> <yourKey> <newTokenAccountName> ACME
```

`<yourADI>` is the name of your ADI (e.g. `bob.acme`)

`<yourKey>` is the label of your key in the CLI

`<newTokenAccountName>` is the name you want your new token account to be (for staking accounts we recommend something like `bob.acme/staking` or `bob.acme/rewards`



### Step 3: Choose the Operator you would like to stake with

Since you are setting up delegated staking, you must choose an Operator to stake with. The following operators are currently accepting stakers:&#x20;

| Operator                 | ADI Name                    |
| ------------------------ | --------------------------- |
| DeFi Devs                | `defidevs.acme`             |
| High Stakes LLC          | `highstakes.acme`           |
| Inveniam                 | `inveniam.acme`             |
| De Facto                 | `defacto.acme`              |
| Sphereon                 | `sphereon.acme`             |
| Kompendium               | `kompendium.acme`           |
| Consensus Networks       | `consensusnetworks.acme`    |
| Factoshi                 | `factoshi.acme`             |
| StampIt                  | `StampIt.acme`              |
| FederateThis             | `FederateThis.acme`         |
| The Factoid Authority    | `TFA.acme`                  |
| LunaNova                 | `LunaNova.acme`             |
| Go Immutable             | `GOI.acme`                  |
| Code Forj                | `codeforj.acme`             |
| ACME Mining              | `ACMEMining.acme`           |
| BetaNode                 | `BetaNode.acme`             |
| Conquistador Mining      | `ConquistadorMining.acme`   |
| Bartow Street Capital    | `BartowStreetCapital.acme`  |
| NiceTouch Communications | `NTC.acme`                  |
| CryptoFund               | `CryptoFund.acme`           |
| CryptoStash              | `CryptoStash.acme`          |
| Pavilion                 | `Pavilion.acme`             |
| Music City Node          | `MusicCityNode.acme`        |
| TurtleBoat               | `TurtleBoat.acme`           |
| OrchardHouse             | `OrchardHouse.acme`         |
| CryptoStake              | `CryptoStake.acme`          |
| AtlantaNode              | `AtlantaNode.acme`          |
| AthensNode               | `AthensNode.acme`           |
| CryptoPoint              | `CryptoPoint.acme`          |
| CryptoPool               | `CryptoPool.acme`           |
| Zeke Investments         | `ZekeInvestments.acme`      |
| Dolphins1972             | `Dolphins1972.acme`         |
| MetisMining              | `MetisMining.acme`          |
| VideFutura               | `VideFutura.acme`           |
| Everest                  | `Everest.acme`              |
| NutshellTechnologies     | `NutshellTechnologies.acme` |
| P16 Redstone             | `p16redstone.acme`          |
| ARSR                     | `arsr.acme`                 |
| PrestigeIT               | `PrestigeIT.acme`           |

****

### Step 4: Run the Delegated Staking Command

#### Run the following command to set up your staking account:

```
accumulate staking convert <stakingAccount> <yourKey> --delegate <operatorUrl> --rewards <rewardsUrl> --type <stakingType>
```

`<`**`stakingAccount`**`>` is the token account you want to use for staking (e.g. `bob.acme/staking`)

`<`**`operatorUrl`**`>` Is the ADI name for the Operator you're choosing to stake with (e.g. `highstakes.acme`)&#x20;

`<`**`rewardsUrl`**`>` Is the token account where you want your staking rewards sent to. You can omit this if you want your rewards sent back to the staking account (make sure to delete the whole `--rewards` flag)

`<`**`stakingType`**`>` is the type of staking account you're setting up (`pure`, `delegated`, `core-validator`, `core-follower`, or `staking-validator`) (default is `inactive`). Since this guide is for setting up delegated staking, you should set this to **`delegated`**.



After running the command, make sure to write down the Transaction Hash. You'll need it for Step 5.

### **Step 5: Submit the Transaction Hash to the Staking Service**

{% hint style="warning" %}
**The staking process cannot be completed until you do this.** The transaction will remain pending until the Staking Service takes custody of your tokens.\

{% endhint %}

The final step is to submit the transaction hash to the Staking Gods. **Submit the transaction hash you received after running the command in Step 4 using the following form**:

{% embed url="https://forms.gle/BtGDU6BYbeBcXr4D8" %}
Send your Transaction Hash in this form
{% endembed %}

### **Step 6: Send the tokens you want to stake to your new Staking Account!**

The final step and the most rewarding (literally!). Send the tokens you want to stake to your token account.&#x20;

You can do this in the CLI using this command:

```
accumulate tx create <fromAddress> <yourKey> <destinationAddress> <amount>
```

`<fromAddress>` is the address for the account where the tokens are coming from

`<yourkey>` is the name of the key that controls the account where the tokens are coming from

`<destinationAddress>` is the address for the account where you want to send the tokens. In this case, this should be your staking account (e.g. `bob.acme/staking`)

{% hint style="danger" %}
Once you send tokens to your staking account, they WILL be locked up for six months. DO NOT send tokens to this account unless you are sure.
{% endhint %}
