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

The TestNet is a secondary production Accumulate network intended for exploratory work. TestNet tokens do not have value. **TestNet history may be reset at any time.**

Currently, the TestNet is hard-coded in `networks.go` as the **`TestNet`** network, with three BVC subnets. The TestNet does not currently include a DC.

## DevNet

`https://devnet.accumulatenetwork.io`

{% hint style="info" %}
DevNet history is reset frequently, by continuous deployment on the `develop` branch.
{% endhint %}

The DevNet is an Accumulate network used for development and validation. The DevNet may be reinitialized, with all history discarded, at any time.

Currently, the DevNet is hard-coded in `networks.go` as the **`DevNet`** network, with three BVC subnets. The DevNet does not currently include a DC.
