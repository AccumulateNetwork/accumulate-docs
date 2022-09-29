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

Currently there are two testnets that are publicly available. A **beta testnet** and a **stable testnet**.

{% tabs %}
{% tab title="Stable testnet" %}
The stable testnet uses the v0.6 tag on Github and Gitlab and will remain so until the mainnet launch.

Endpoint: `https://testnet.accumulatenetwork.io/v2`

* CLI branch: `develop`
* You can use the Accumulate explorer to view the transactions on this version of the network at the main mirror (explorer.accumulatenetwork.io)
{% endtab %}

{% tab title="Beta testnet" %}
The beta testnet uses the v0.7 tag on Github and Gitlab.

* Endpoint: `https://beta.testnet.accumulatenetwork.io/v2`
* CLI branch: `cli-v1.0.0-rc3.1` and the tag deployed `v1-0-0-rc3.1`

You can use the Accumulate explorer to view transactions on this network version at [beta.explorer.accumulatenetwork.io](https://beta.explorer.accumulatenetwork.io).
{% endtab %}
{% endtabs %}

## Devnet

{% hint style="warning" %}
NOTICE: The Devnet is now deprecated. The below information is no longer valid, and will be removed soon. You can still set up a Local Devnet - see [local-devnet.md](../setup/local-devnet.md "mention") for details.
{% endhint %}

`https://devnet.accumulatenetwork.io`

The devnet is an Accumulate network used for development and validation. It is more bleeding edge than the testnets, and is constantly updated. The devnet may be reinitialized, with all history discarded, at any time.

The devnet uses the `develop` branch. There is a publicly available endpoint: `devnet.accumulatenetwork.io`. You can also set up your own local devnet (see [local-devnet.md](../setup/local-devnet.md "mention")for instructions).

You can use the Accumulate explorer to view transactions on this version of the network at[ ](https://dev.explorer.accumulatenetwork.io/)[https://dev.explorer.accumulatenetwork.io/](https://dev.explorer.accumulatenetwork.io/).

Since the devnet is changing rapidly, we encourage you to use the stable testnet or beta testnet.
