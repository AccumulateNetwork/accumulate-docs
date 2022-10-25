# Networks

## Mainnet

The mainnet is the primary Accumulate network.

{% hint style="info" %}
The mainnet will not be launched until testing and development is done, currently scheduled for October, 2022.
{% endhint %}

## Testnet

{% hint style="info" %}
Testnet history may be reset at the discretion of DeFi Devs. Generally, this will happen for minor releases or history-breaking bugs.
{% endhint %}

The testnet is a secondary production Accumulate network intended for exploratory work. Testnet tokens do not have value. Testnet history may be reset at any time.

Currently, there are two testnets that are publicly available. A **beta testnet** and a **stable testnet**.

{% tabs %}
{% tab title="Stable testnet" %}
The stable testnet uses the `main` branch on Gitlab.

* The stable testnet endpoint is `https://testnet.accumulatenetwork.io/v2`
* To use the CLI with the Stable Testnet, you must check out the `main` branch on the `wallet` repository ([`gitlab.com/accumulatenetwork/core/wallet`](https://gitlab.com/accumulatenetwork/core/wallet)).
* Using the [Accumulate explorer](https://explorer.accumulatenetwork.io/), you can view the transactions on this network version.
{% endtab %}

{% tab title="Beta testnet" %}
{% hint style="warning" %}
DEPRECATED
{% endhint %}

\
The beta testnet uses the v0.7 tag on Github and Gitlab.

* Endpoint: `https://beta.testnet.accumulatenetwork.io/v2`
* CLI branch: `cli-v1.0.0-rc3.1` and the tag deployed `v1-0-0-rc3.1`

You can use the Accumulate explorer to view transactions on this network version at [beta.explorer.accumulatenetwork.io](https://beta.explorer.accumulatenetwork.io).
{% endtab %}
{% endtabs %}
