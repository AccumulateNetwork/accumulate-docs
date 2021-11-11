# Networks

## MainNet

The MainNet is the primary Accumulate network.

{% hint style="danger" %}
The MainNet will not be created until testing and development is done
{% endhint %}

## TestNet

The TestNet is a secondary production Accumulate network intended for exploratory work. TestNet tokens do not have value. **TestNet history may be reset at any time.**

Currently, the TestNet is hard-coded in `networks.go` as the **`TestNet`** network, with three BVC subnets. The TestNet does not currently include a DC.

## DevNet

The DevNet is an Accumulate network used for development and validation. The DevNet may be reinitialized, with all history discarded, at any time.

Currently, the DevNet is hard-coded in `networks.go` as the **`DevNet`** network, with three BVC subnets. The DevNet does not currently include a DC.
