# Networks

## MainNet

The MainNet is the primary Accumulate network.

{% hint style="danger" %}
The MainNet will not be created until testing and development is done
{% endhint %}

## TestNet

`https://testnet.accumulatenetwork.io`

{% hint style="info" %}
TestNet history may be reset at the discretion of DeFi Devs. Generally, this will happen for minor releases or history-breaking bugs.
{% endhint %}

The TestNet is a secondary production Accumulate network intended for exploratory work. TestNet tokens do not have value. TestNet history may be reset at any time.

**Types Of Testnet**

* Stable Testnet
* Beta Testnet

{% tabs %}
{% tab title="Stable Testnet" %}
The stable testnet uses the v0.6 tag on Github and Gitlab and will remain so until the mainnet launch.&#x20;

* Endpoint: `testnet.accumulatenetwork.io`
* CLI branch: `cli-v0.6`

You can use the Accumulate explorer to view the transactions on this version of the network at the main mirror ([explorer.accumulatenetwork.io](https://explorer.accumulatenetwork.io))
{% endtab %}

{% tab title="Beta Testnet" %}
The beta testnet uses the v0.7 tag on Github and Gitlab.&#x20;



* Endpoint: `beta.testnet.accumulatenetwork.io`
* CLI branch: `cli-0.7.0-beta`

&#x20;You can use the Accumulate explorer to view transactions on this version of the network at [beta.explorer.accumulatenetwork.io](https://beta.explorer.accumulatenetwork.io).
{% endtab %}
{% endtabs %}

## DevNet

`https://devnet.accumulatenetwork.io`

{% hint style="info" %}
DevNet history is reset frequently, by continuous deployment on the `develop` branch and devnet is bleeding edge and very unstable.
{% endhint %}

The DevNet is an Accumulate network used for development and validation. The DevNet may be reinitialized, with all history discarded, at any time.

The devnet uses the `develop branch` and the endpoint is You can use the Accumulate explorer to view transactions on this version of the network at[ ](https://dev.explorer.accumulatenetwork.io/)[https://dev.explorer.accumulatenetwork.io/](https://dev.explorer.accumulatenetwork.io/).

Since the devnet is changing rapidly, we encourage you to use the stable or beta testnet.
