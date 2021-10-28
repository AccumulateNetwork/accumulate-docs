---
description: >-
  This guide will run you through how to create a Validator Node to an
  Accumulate network.
---

# Validator Node Setup Guide

{% hint style="info" %}
This guide is for creating a Validator node on Accumulate, which participates in consensus. If you would like to set up a follower node instead, which only records transactions on the network, please see the [follower-node-setup-guide.md](follower-node-setup-guide.md "mention").
{% endhint %}

{% hint style="warning" %}
Accumulate is not currently set up in a way that allows operators outside of the core team to join the network as validators. This guide is not useful without access to DeFi Dev's cloud infrastructure.
{% endhint %}

## BVC

{% hint style="info" %}
`<network>` must be the name of BVC network and `<all networks>` must be a comma-separated list of all BVC networks. See [networks.md](networks.md "mention") for a list of BVC network names.
{% endhint %}

1. Execute the following command to configure a BVC network: `accumulated init --work-dir .nodes --network "<network>" --relay-to "<all networks>"`
2. Copy `.nodes` to each server
3. On each server, execute `accumulated run --work-dir .nodes -n <node number>`. `<node number>` must be the index of the node's IP address in the network's `Nodes` array (in `networks.go`).
